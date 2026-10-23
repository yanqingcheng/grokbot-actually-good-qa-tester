# Grok Bot box: sound and speech

Open only when the charter's readiness list (or setup) names sound or speech. General box notes and leases: `machine-setup/references/grok-bot-box.md`. Run commands from your session folder.

## Recording sound

The box may have a shared sound server with a virtual speaker, `virtual_out` (its socket path is in your house rules or setup; written `<sound-server socket>` below). Chrome plays into it; you record from `virtual_out.monitor`.

1. Check it's there: `[ -S <sound-server socket> ] && PULSE_SERVER=unix:<sound-server socket> pactl list short sinks` should list `virtual_out`. If the socket is missing and your machine has a recovery script, your house rules name it. If the socket, `pactl` or `parecord` is still missing, sound can't be recorded on this box yet: record it as a gap in your machine state and readiness, and tell your manager. Never claim sound was checked.
2. **It is shared, so only attributable sound is evidence.** Other agents' sound can play into the same speaker and land in your recording. Sound counts as evidence only when, at that moment, the one stream playing was your own Chrome: run `PULSE_SERVER=unix:<sound-server socket> pactl list sink-inputs` and log, with the time, each stream's `application.process.id`; it must belong to your Chrome (`ps -o pid,ppid,comm -p <id>` leads back through `chrome` to your own script's pid). Playwright may not give you Chrome's pid; log your script's `process.pid` at launch and find Chrome as its child (`ps -o pid,comm --ppid <script pid>`). If another stream was playing, that stretch of the recording can't be attributed: say so and repeat. If your house rules or manager give you a dedicated speaker of your own, use it instead.
3. Give Chrome the server in its own environment, unmuted:
   ```js
   const { chromium } = require('playwright-core');           // only playwright-core is installed
   chromium.launch({ executablePath: '/usr/bin/google-chrome',
     ignoreDefaultArgs: ['--mute-audio'],                      // Playwright mutes by default
     env: { ...process.env, PULSE_SERVER: 'unix:<sound-server socket>' } })
   ```
   Autoplay: adding `args: ['--autoplay-policy=no-user-gesture-required']` lets a page play sound with no click. Use it only to prove capture works, or to reach sound you're testing for another reason. The product's real autoplay behaviour is a user-facing behaviour: test it without the flag, as a visitor's browser would.
4. Record: `PULSE_SERVER=unix:<sound-server socket> parecord --device=virtual_out.monitor --latency-msec=50 --file-format=wav audio/rec-01.wav &` then `echo $! > audio/rec-01.pid`, and log the clock time it started. Stop it with `kill -INT` on that pid only after the sound has finished, and wait for it to exit, as for video. Stopped too early, it leaves a header-only file (44 bytes): check the size before trusting it.
5. Check the capture: `ffmpeg -i audio/rec-01.wav -af volumedetect -f null - 2>&1 | grep -E 'mean_volume|max_volume'`. Silence reads around -91 dB; a loud test tone reads close to 0 dB (illustration: -3 dB mean). A level shows that something played, not what: tie it to your own stream (step 2), and listen or compare with what the page should play.

## Speech (text-to-speech voices)

1. Check the tools exist: `command -v espeak-ng speech-dispatcher`.
2. Start Chrome with `--enable-speech-dispatcher`. Without it, `speechSynthesis.getVoices()` reports 0 voices. That is a tool setting, not proof that speech can't be tested.
3. Wait for the `voiceschanged` event (or poll for a few seconds) before counting voices. They load late.
4. Log the default voice (`getVoices()[0]` and its `lang`). A page that sets no voice or language gets that one.
5. Record the speech with the sound recipe above.
6. Starting Chrome this way can start a `speech-dispatcher` process. Note its pid when it starts. Stop it in cleanup if your run started it.
