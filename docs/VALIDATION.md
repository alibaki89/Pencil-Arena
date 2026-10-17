# Manual browser acceptance checklist

Run on desktop Chrome and Firefox (WebGL enabled), with a fresh profile and saved settings. Mark each scenario PASS/FAIL with screenshots/notes. These tests were **not** completed by the automated audit.

- [ ] Launch/start from entry menu; pointer lock and aim work
- [ ] Move/jump/crouch/slide/vault/climb over representative geometry
- [ ] Switch weapon, fire, reload and scope; hit indicators update
- [ ] Enemy waves spawn, chase, attack and die appropriately
- [ ] Damage/health/ammo/score persist in expected states
- [ ] Check collision at doors, corners, stairs, windows and indoor camera
- [ ] Pause/resume; Alt-Tab; pointer lock returns predictably
- [ ] Verify adaptive resolution under a busy combat scene
- [ ] Verify menu and paused GPU load, no stuck or stretched canvas

## Measurement instructions

1. Open Chrome Developer Tools → Performance and capture 30 seconds during active gameplay and 30 seconds paused.
2. Compare frame count and GPU activity against the original release on the same hardware; expect non-gameplay draw frequency to fall toward 10 Hz, not a claimed measured FPS gain.
3. Test at 1280×720 and 1920×1080, low- and high-DPR displays if available.
4. Record browser, OS, GPU, seed, mode and result when filing a bug.

## Automated smoke test

`node tests/verify.mjs`

This validates self-containment and parsing, not full WebGL gameplay.

## Completed virtual-desktop smoke checks

- WebGL canvas initialized in original and revised Chromium runs; intro and main menu displayed.
- `window.__arena.probe()` returned normal initial position, grounded character, valid layout access.
- Isolated idle draw-request count: original 65, release 18 over an approximately 3.6-second window. Not an FPS benchmark.
