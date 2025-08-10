
# No Sleep (Keep Screen On)

A tiny single-file web app that keeps the screen awake while the page is open. It uses the Screen Wake Lock API when available and automatically falls back to NoSleep.js for browsers that don't support it (e.g., iOS Safari).

- File: `no-sleep.html`
- Fallback: [NoSleep.js](https://github.com/richtr/NoSleep.js) via CDN
- Works best over HTTPS; requires a user gesture (button click)

---

## Features

- Toggle keep-awake on/off with a single button
- Uses Screen Wake Lock API when supported
- Automatic fallback to NoSleep.js when not supported
- Auto re-requests wake lock when the tab becomes visible again
- Clear status indicator (Off / On with API or Fallback)

---

## How it works

1. Tries `navigator.wakeLock.request('screen')` (Screen Wake Lock API).
2. If unsupported or fails, enables NoSleep.js which prevents auto-lock by playing a tiny hidden video (mobile-friendly fallback).
3. Listens to `visibilitychange` to restore keep-awake after tab switches.

---

## Getting started

### Option 1: Open locally
- Download `no-sleep.html` and open it in your browser by double-clicking.
- Note: Some browsers require a secure context for Wake Lock. If the native API doesn’t work locally, the fallback will still work in most cases.

### Option 2: Serve over HTTPS
- Host the file on any HTTPS server (recommended for maximum compatibility).

Quick local server examples (development only):
```bash
# Python 3
python -m http.server 8000

# Node (using http-server)
npx http-server -p 8000
```
Then open http://localhost:8000/no-sleep.html

---

## Usage

1. Click “Enable” to keep the screen awake.
2. The status will show:
   - “On (Screen Wake Lock)” when native API is active
   - “On (Fallback: NoSleep.js)” when using fallback
3. Click “Disable” to stop.
4. If you switch apps/tabs and come back, the page will attempt to restore wake lock automatically.

---

## Browser compatibility

- Chrome/Edge/Opera/Android browsers: Screen Wake Lock API generally supported.
- Safari (iOS/iPadOS): Native API not supported as of now; fallback (NoSleep.js) is used.
- Desktop Safari/Firefox: Support varies; fallback will be used if native API is unavailable.

Notes and limitations:
- A user gesture is required (click the button).
- Low Power Mode / Battery Saver may interfere.
- The API keeps the screen awake; it does not guarantee preventing full device sleep under all OS policies.
- Backgrounding the tab or locking the device will release native wake locks; the page tries to restore when visible again.

---

## Customization

- Text/UI: Edit labels in the HTML.
- Styles: Tweak CSS variables, colors, or fonts in the `<style>` section.
- Primary color: Change the button background color (`#0a7cff`).
- Self-host NoSleep.js:
  ```html
  <script defer src="/path/to/NoSleep.min.js"></script>
  ```
  You can obtain it via:
  - Download from https://github.com/richtr/NoSleep.js
  - Or install: `npm i nosleep.js` and use `node_modules/nosleep.js/dist/NoSleep.min.js`

---

## Troubleshooting

- “Wake Lock API not supported”:
  - Expected on Safari/iOS. The page will switch to NoSleep.js automatically.
- “Released, will retry when visible”:
  - The system/app/tab temporarily released the lock. It will retry when you return to the tab.
- Doesn’t work on iOS:
  - Ensure you clicked “Enable.”
  - Keep the page in the foreground.
  - Disable Low Power Mode if possible.
  - iOS can still enforce auto-lock in some scenarios; the fallback mitigates most cases but cannot override all system policies.

---

## Privacy & security

- The page doesn’t collect or send any data.
- Loads NoSleep.js from a public CDN by default; you can self-host to avoid external requests.
- Screen Wake Lock requires a secure context (HTTPS) in most browsers.

---

## License

- This page: You may use and modify freely for your own projects.
- NoSleep.js: MIT License (see the NoSleep.js repository for details).

---

## 한국어 안내 (Korean)

이 페이지는 화면이 꺼지지 않도록 유지하는 간단한 웹 앱입니다. 지원 브라우저에서는 Screen Wake Lock API를 사용하고, 미지원 브라우저(iOS Safari 등)에서는 자동으로 NoSleep.js로 폴백합니다.

- 파일: `no-sleep.html`
- HTTPS 환경에서 가장 안정적으로 동작하며, 버튼 클릭 등 사용자 동작이 필요합니다.

사용 방법:
1) “Enable” 버튼을 누르면 화면 항상 켜짐이 활성화됩니다.
2) 상태 표시로 네이티브 API 또는 폴백(NoSleep.js) 사용 여부를 확인할 수 있습니다.
3) 앱/탭 전환 후 돌아오면 자동 복구를 시도합니다.
4) “Disable”로 비활성화할 수 있습니다.

알려진 제약:
- iOS에서는 네이티브 API 미지원으로 폴백 사용.
- 저전력 모드/배터리 세이버에서 동작이 제한될 수 있습니다.
- 운영체제 정책상 완전한 기기 절전 방지는 보장되지 않습니다.

커스터마이즈:
- 문구/스타일을 HTML/CSS에서 자유롭게 수정하세요.
- NoSleep.js를 로컬로 호스팅해 외부 요청 없이 사용할 수 있습니다.

라이선스:
- 본 예제는 자유롭게 사용/수정 가능.
- NoSleep.js는 MIT 라이선스입니다.
