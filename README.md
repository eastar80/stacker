# STACKER

원버튼 블록 스태킹 게임. 탭/스페이스로 움직이는 블록을 쌓고, 어긋난 만큼 잘려나간다.
판정 범위 안에 딱 맞추면 PERFECT 콤보 — 점수 보너스와 함께 블록 폭이 회복된다.

## 난이도

시작 화면에서 고른다. 선택은 저장되어 다음 판에도 유지된다.

| | 뜻 | 블록 속도 | PERFECT 판정 | 폭 회복 |
|---|---|---|---|---|
| **FOUNDATION** | 토대 | 2.6 → 5.6 | 10px | +6px |
| **SKYLINE** | 스카이라인 | 3.2 → 7.4 | 7px | +4px |
| **VERTIGO** | 현기증 | 4.0 → 9.4 | 5px | +2px |
| **BABEL** | 바벨 | 5.0 → 11.8 | 3px | 없음 |

속도는 층이 올라갈수록 빨라져 표의 최대치에서 멈춘다. `SKYLINE` 이 기존 기본값이고,
`BABEL` 은 폭 회복이 없어 한 번 좁아지면 되돌릴 수 없다.

점수는 착지 1점, PERFECT 는 `1 + 콤보` 점이다 (첫 PERFECT 2점, 연속으로 3점, 4점 …).
좌측 상단 패널이 이 규칙과 **다음 PERFECT 로 얻을 점수**를 실시간으로 보여준다.

리더보드 기록에는 어느 난이도에서 낸 점수인지 함께 남는다.

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
  - 효과음도 Web Audio 합성이다. PERFECT 는 콤보마다 반음 올라가는 상승 아르페지오,
    어긋난 착지는 둔탁한 충격음, 게임 오버는 단조 3음 하강 뒤 바닥 충격.
  - 우측 상단 버튼은 음악과 효과음을 함께 끈다.

## 저장

리더보드는 저장 어댑터를 통해 환경에 맞게 저장된다:
1. `window.storage` — Claude.ai 아티팩트 환경
2. `localStorage` — 일반 브라우저 (배포 시 이 경로 사용)
3. 메모리 — 둘 다 불가할 때 폴백

저장 키는 리더보드(`stacker-leaderboard`), 마지막 이름(`stacker-lastname`),
난이도 선택(`stacker-difficulty`) 세 개다.

## 로드맵

- [ ] 파일 분리 (game.js / audio.js / storage.js / style.css)
- [x] GitHub Pages 배포 — `main` 푸시 시 자동 (`.github/workflows/pages.yml`)
- [ ] 온라인 공유 리더보드 (백엔드 필요 — CLAUDE.md 참고)
- [ ] 모바일 최적화 점검 (터치 지연, 세로 화면 레이아웃)
