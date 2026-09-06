# STACKER

원버튼 블록 스태킹 게임. 탭/스페이스로 움직이는 블록을 쌓고, 어긋난 만큼 잘려나간다.
7px 이내로 딱 맞추면 PERFECT 콤보 — 점수 보너스와 함께 블록 폭이 살짝 회복된다.

## 실행

배포판: https://eastar80.github.io/stacker/

빌드 과정 없음. 정적 HTML 한 파일이 전부다.

```bash
# 브라우저에서 바로 열기
open index.html          # macOS
start index.html         # Windows

# 또는 로컬 서버로
npx serve .
```

## 구조

- `index.html` — 게임 전체 (HTML + CSS + JS 단일 파일)
  - Canvas 렌더링, Web Audio 칩튠 시퀀서(음원 파일 없음), TOP 5 리더보드

## 저장

리더보드는 저장 어댑터를 통해 환경에 맞게 저장된다:
1. `window.storage` — Claude.ai 아티팩트 환경
2. `localStorage` — 일반 브라우저 (배포 시 이 경로 사용)
3. 메모리 — 둘 다 불가할 때 폴백

## 로드맵

- [ ] 파일 분리 (game.js / audio.js / storage.js / style.css)
- [x] GitHub Pages 배포 — `main` 푸시 시 자동 (`.github/workflows/pages.yml`)
- [ ] 온라인 공유 리더보드 (백엔드 필요 — CLAUDE.md 참고)
- [ ] 모바일 최적화 점검 (터치 지연, 세로 화면 레이아웃)
