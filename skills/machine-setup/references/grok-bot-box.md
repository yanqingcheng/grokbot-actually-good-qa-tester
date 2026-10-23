# Grok Bot platform reference: recipes for the Grok Bot box

Only if you run as a Grok Bot. Recipes for a Grok Bot box: a shared Linux computer with Chrome and ffmpeg, and sometimes a sound server. Your house rules add paths, leases and limits. On other hosts, skip it and prove your own tools ("Prove your tools" in [machine-setup](../../machine-setup/SKILL.md)).

- Prove before you rely on it. Each recipe starts with a check. If a check fails or names differ, tell your manager. Don't conclude the capability is missing. A safe equivalent that gives evidence as good for the mission is fine: prove it the same way and say what you used.
- Follow the session rules first (`test-session/references/session-rules.md` and `test-session/references/resource-cleanup.md`): memory floor, leases, cleanup. The box is shared: leave headroom for heavy missions, try recipes on something harmless first, and stop only your own processes, by pid.
- Values are working examples. Take screen sizes from your charter. Change the frame rate, overlay, `--latency-msec=50` or polling delays if you need to, and re-prove the recipe.

Run commands from your session folder. First: `mkdir -p shots video audio`.

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
For a desktop setting, use the size from your charter (illustration: `{ viewport: { width: 1280, height: 800 } }`) without `isMobile`/`hasTouch`. At phone size, a page with no `<meta name="viewport">` tag lays out at 980 px wide (`innerWidth` 980) while the screen is 390: that's how real phones render it too, so judge it as a finding, not a tool fault. Leave out `headless: false` for a headless run (faster, but a screen recording can't see it).

Playwright's own video (`recordVideo`) does not work here: its bundled ffmpeg is missing ("Executable doesn't exist at …/ms-playwright/ffmpeg-…"). For a headless run, use "Recording a headless browser" below.

## Recording the screen with a clock (headed browser)

Check: `echo "$DISPLAY"` is set (your desktop's own display) and `ls /usr/share/fonts/truetype/dejavu/DejaVuSansMono-Bold.ttf`.

Start ffmpeg itself in the background and save its own pid:
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

## Recording a headless browser

Headless browsers have no display to grab. Record the page through Chrome's screencast and burn in the clock with the system ffmpeg (Check: `ffmpeg -hide_banner -filters | grep drawtext`). In your script, after `newPage()`:
```js
const fs = require('fs'); fs.mkdirSync('video/frames-01', { recursive: true });
const cdp = await ctx.newCDPSession(page); let n = 0, stopped = false;
cdp.on('Page.screencastFrame', f => {
  if (stopped) return;   // frames still in flight after stop must not be written
  fs.writeFileSync(`video/frames-01/${String(n++).padStart(6, '0')}-${Math.round(f.metadata.timestamp * 1000)}.jpg`, Buffer.from(f.data, 'base64'));
  cdp.send('Page.screencastFrameAck', { sessionId: f.sessionId }).catch(() => {});
});
await cdp.send('Page.startScreencast', { format: 'jpeg', quality: 80 });
try {
  // … probes …
} finally {
  stopped = true; await cdp.send('Page.stopScreencast').catch(() => {});   // before browser.close()
}
```
Frames arrive only when the page repaints, and each file name carries its wall-clock time in ms. Build the clip with each frame shown until the next, and the clock taken from those times:
```
cd video && python3 - frames-01 <<'PY'
import os, sys; d = sys.argv[1]; fs = sorted(os.listdir(d)); t = [int(f.split('-')[1][:-4]) for f in fs]
with open(d + '.txt', 'w') as o:
    for i, f in enumerate(fs): o.write(f"file '{d}/{f}'\nduration {((t[i+1] - t[i]) / 1000 if i + 1 < len(fs) else 0.5):.3f}\n")
    o.write(f"file '{d}/{fs[-1]}'\n")
open(d + '.start', 'w').write(f"{t[0] / 1000:.3f}")
PY
START=$(cat frames-01.start)
ffmpeg -loglevel error -f concat -safe 0 -i frames-01.txt -vf "drawtext=fontfile=/usr/share/fonts/truetype/dejavu/DejaVuSansMono-Bold.ttf:text='%{pts\:localtime\:$START\:%H\\\\\:%M\\\\\:%S}':x=w-tw-10:y=10:fontsize=22:fontcolor=yellow:box=1:boxcolor=black@0.7,fps=10" -c:v libx264 -preset ultrafast -pix_fmt yuv420p -y rec-01.mp4
```
Then decode-check it and look at the clock frame as for a headed recording above. A screenshot per step plus a script log with clock times is a fallback only if it is just as good for the mission (no motion, timing or fleeting states to show); otherwise agree a narrower mission first (step 8 of [write-charter](../../write-charter/SKILL.md)). If your house rules provide a screencast helper, use it as they say, and decode-check its clips as above before trusting them.

Sound and speech recipes: `machine-setup/references/grok-bot-box-sound.md`, opened only when the charter's readiness list names sound or speech.

## Leases

General rule: "Leases and locks" in `test-session/references/resource-cleanup.md`. If your house rules provide a shared-box lease tool, take a lease before you launch a browser, renew it before it expires, and release it after closing the browser. Never launch without one when the house rules require it. Recording needs no lease of its own.
4. Never leave a browser open between turns or runs.

## Secrets

Use Grok Bot's built-in secret handling: ask for a secret through a secret request, and it reaches you as an environment variable you use by name (illustration: `process.env.SHOP_QA_PASSWORD` in your script). The secrets ban (never printed, never in chat, logs, notes, evidence or files): "Secrets" in `test-session/references/session-rules.md`.
