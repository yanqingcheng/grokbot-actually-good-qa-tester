# Grok Bot platform reference: recipes for the Grok Bot box

**Optional platform reference, only if your tester runs as a Grok Bot.** Every Grok Bot has the same box (a shared Linux computer with Chrome, ffmpeg and a sound server), so these recipes should work for any Grok Bot tester. Nothing here is specific to one owner or host: your own house rules add your paths, leases and limits. On any other host, skip this file and prove your own tools the same way (see "prove your tools" in [qa-tester-getting-started](../../qa-tester-getting-started/SKILL.md)).

**Prove before you rely on it.** Each recipe starts with a check that what it needs exists. If a check fails or the names differ, tell your manager; don't decide the capability doesn't exist, and don't improvise around it. The recipes were checked on the box on 22 Oct 2026. Follow the resource and safety rules first (memory floor, any lease your house rules require, cleanup; `references/session-rules.md` of [qa-tester-test-session](../../qa-tester-test-session/SKILL.md)). The box is shared, so a tool that took the last of its memory would starve every other agent: keep to your memory floor and any limit your host's tools enforce, and leave extra headroom if your mission needs more than usual, and try recipes on something harmless you control before a real session. The box is shared with other agents: stop only your own processes, by their own pid. Your house rules may add tools and limits. **Values in these recipes are working examples:** take screen sizes from your charter; the frame rate, overlay font and position, `--latency-msec=50` and polling delays are what worked in the 22 Oct checks, so change them if your capture needs differ, and re-prove the recipe if you do.

Commands below run from your session folder; create the folders first: `mkdir -p shots video audio`.

## Driving Chrome with Playwright

Check: `ls /usr/bin/google-chrome && ls "$(npm root -g)/playwright-core"`.

Use the system Chrome and the box-wide `playwright-core`; don't install your own copy. Run with `NODE_PATH=$(npm root -g) node script.js`. A complete minimal script that runs headed (visible on your desktop, so a screen recording can see it) at phone size with touch:
```js
const { chromium } = require('playwright-core');
(async () => {
  const browser = await chromium.launch({ executablePath: '/usr/bin/google-chrome', headless: false });
  try {
    const ctx = await browser.newContext({ viewport: { width: 390, height: 844 }, isMobile: true, hasTouch: true });
    const page = await ctx.newPage();
    console.log(new Date().toTimeString().slice(0, 8), 'open'); await page.goto('about:blank');
    await page.screenshot({ path: 'shots/01-start.png' });
  } finally { await browser.close(); }   // always close, even on failure
})();
```
For a desktop setting, use the size from your charter (illustration: `{ viewport: { width: 1280, height: 800 } }`) without `isMobile`/`hasTouch`. Leave out `headless: false` for a headless run (faster, but a screen recording can't see it).

**Playwright's own video (`recordVideo`) does not work on the box**: it looks for Playwright's bundled ffmpeg, which isn't installed ("Executable doesn't exist at …/ms-playwright/ffmpeg-…"). Record another way:

## Recording the screen with a clock (headed browser)

Check: `echo "$DISPLAY"` is set (your desktop's own display) and `ls /usr/share/fonts/truetype/dejavu/DejaVuSansMono-Bold.ttf`.

Start ffmpeg itself in the background and save **its own** pid:
```
ffmpeg -loglevel error -f x11grab -video_size 1280x800 -framerate 10 -i "$DISPLAY" -vf "drawtext=fontfile=/usr/share/fonts/truetype/dejavu/DejaVuSansMono-Bold.ttf:text='%{localtime\:%H\\\\\:%M\\\\\:%S}':x=w-tw-10:y=10:fontsize=22:fontcolor=yellow:box=1:boxcolor=black@0.7" -c:v libx264 -preset ultrafast -pix_fmt yuv420p -y video/rec-01.mp4 > video/rec-01.log 2>&1 &
echo $! > video/rec-01.pid
```
Stop it by that pid only, wait for it to finish writing, then check the file:
```
PID=$(cat video/rec-01.pid); kill -INT "$PID"; while kill -0 "$PID" 2>/dev/null; do sleep 0.5; done
ffmpeg -v error -i video/rec-01.mp4 -f null -                    # no output = the whole clip decodes
ffprobe -v error -show_entries format=duration -of csv=p=0 video/rec-01.mp4
ffmpeg -loglevel error -i video/rec-01.mp4 -frames:v 1 -y shots/clock-check.png   # then look at the clock
```
Never stop a recorder by name or pattern: other agents record on the box too.

**Headless browsers** have no display to grab. Run headed for the parts you need on video. A screenshot per step plus a script log with clock times is a fallback only if it is just as good for the mission (no motion, timing or fleeting states to show); otherwise agree a narrower mission first ("Plan and get resources" in [qa-tester-test-session](../../qa-tester-test-session/SKILL.md)). If your house rules provide a screencast helper, use it as they say, and decode-check its clips as above before trusting them.

## Recording sound

The box has a shared sound server with a virtual speaker, `virtual_out`. Chrome plays into it; you record from `virtual_out.monitor`.

1. **Check it's there:** `[ -S /tmp/pulse-shared/native ] && PULSE_SERVER=unix:/tmp/pulse-shared/native pactl list short sinks` should list `virtual_out`. If not, tell your manager.
2. **It is shared, so only attributable sound is evidence.** Other agents' sound can play into the same speaker and land in your recording. Sound counts as evidence only when, at that moment, the one stream playing was your own Chrome: run `PULSE_SERVER=unix:/tmp/pulse-shared/native pactl list sink-inputs` and log, with the time, each stream's `application.process.id`; it must belong to your Chrome (`ps -o pid,ppid,comm -p <id>` leads back through `chrome` to your own script's pid). If another stream was playing, that stretch of the recording can't be attributed: say so and repeat. If your house rules or manager give you a dedicated speaker of your own, use it instead.
3. **Give Chrome the server in its own environment, unmuted:**
   ```js
   chromium.launch({ executablePath: '/usr/bin/google-chrome',
     ignoreDefaultArgs: ['--mute-audio'],                      // Playwright mutes by default
     env: { ...process.env, PULSE_SERVER: 'unix:/tmp/pulse-shared/native' } })
   ```
   **Autoplay:** adding `args: ['--autoplay-policy=no-user-gesture-required']` lets a page play sound with no click. Use it only to prove capture works, or to reach sound you're testing for another reason. The product's real autoplay behaviour is a user-facing behaviour: test it **without** the flag, as a visitor's browser would.
4. **Record:** `PULSE_SERVER=unix:/tmp/pulse-shared/native parecord --device=virtual_out.monitor --latency-msec=50 --file-format=wav audio/rec-01.wav &` then `echo $! > audio/rec-01.pid`, and log the clock time it started. Stop it with `kill -INT` on that pid and wait for it to exit, as for video.
5. **Check the capture:** `ffmpeg -i audio/rec-01.wav -af volumedetect -f null - 2>&1 | grep -E 'mean_volume|max_volume'`. Silence reads around -91 dB; in the 22 Oct check, a test tone read -3 dB mean. A level shows that something played, not what: tie it to your own stream (step 2), and listen or compare with what the page should play.

## Speech (text-to-speech voices)

Check first: `command -v espeak-ng speech-dispatcher`. Chrome started with no flags reports `speechSynthesis.getVoices()` as 0 voices; start it with `--enable-speech-dispatcher` and it lists the espeak-ng voices (seen 22 Oct 2026). Voices load late, so wait for the `voiceschanged` event (or poll for a few seconds) before counting them. The box's default voice is not English (it was Afrikaans on 22 Oct), so a page that sets no voice or language gets that one. Record the speech with the sound recipe above. Starting Chrome this way can start a `speech-dispatcher` process; note its pid when it starts and stop it in cleanup if your run started it. "0 voices" without the flag is a tool setting, not proof that speech can't be tested.

## Driver timing

A browser subagent on the box has been seen to take roughly 20 s between separate actions (an observation, not a guarantee: measure your own). Gaps much shorter than that need the second action pre-staged or a script.

## Secrets

Use Grok Bot's built-in secret handling: ask for a secret through a secret request, and it reaches you as an environment variable you use by name (illustration: `process.env.SHOP_QA_PASSWORD` in your script). Never write a secret to a file, notes, logs or chat, and never print it.
