# Snapora — Screenshot & Screen Recorder

Local-first MV3 screenshot + recorder for Chrome and Brave. No backend, no tracking, no remote code.

## Install (Developer Mode)

1. Build: `npm.cmd install` then `npm.cmd run build`
2. Chrome: open `chrome://extensions` → Developer mode → Load unpacked → select `dist/`
3. Brave: open `brave://extensions` → Developer mode → Load unpacked → select `dist/`

## Permissions and why

| Permission | Reason |
|---|---|
| `activeTab` | Capture the visible tab the user invoked the action on |
| `scripting` | Inject area-select / full-page helpers on http(s) pages only |
| `tabCapture` / `desktopCapture` | Record tab, screen, or window (user picks each time) |
| `downloads` | Save screenshots / recordings locally |
| `storage` | Settings + drafts on device |
| `clipboardWrite` | Copy annotated image to clipboard |
| `http://*/* https://*/*` (host) | Content-script helpers for full-page stitching |

No `all_urls`, no remote hosts, no API keys. Pages like `chrome://`, Web Store, and browser internals cannot be captured — the popup says so instead of crashing.

## Build

- `npm.cmd run typecheck` — strict TypeScript
- `npm.cmd test` — unit tests (8 green)
- `npm.cmd run build` — vite build + `dist/` packaging + manifest validation

## Credits

- MP4 conversion: [mediabunny](https://github.com/Vanilagy/mediabunny) (MPL-2.0), bundled unmodified, loaded lazily only on MP4 export.

## Honest limits

- System audio depends on OS/browser/source; if unavailable the recording continues without it and says so.
- 4K is offered but the UI reports the real height; no fake 4K claim.
- MP4 export is real (WebM → H.264/AAC via mediabunny + WebCodecs, 100% local, lazy-loaded) but needs a browser H.264 encoder — most Chrome/Brave installs qualify; otherwise you get a clear message and keep the WebM.
- Video trimming here is preview/frame tools plus MP4 conversion; no FFmpeg (RAM stays low).
