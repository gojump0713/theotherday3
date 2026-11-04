# TheOtherDay 2026 행사 스크린 — 운영 매뉴얼

가로 16:9 (1920×1080) 단일 HTML. 인터넷 없이 동작합니다.

## 배포 URL

https://gojump0713.github.io/theotherday3/ (GitHub Pages, main 푸시 시 자동 배포). 현장 송출은 네트워크 변수를 피하기 위해 이 폴더의 로컬 복사본을 권장합니다.

## 실행

1. `screen` 폴더째 송출 PC로 복사
2. Chrome/Edge 키오스크 모드로 실행 (예시, 경로는 실제 위치로 변경)

```
"C:\Program Files\Google\Chrome\Application\chrome.exe" --kiosk --autoplay-policy=no-user-gesture-required "file:///D:/screen/index.html?clean=1#idle"
```

- `--autoplay-policy=no-user-gesture-required` : 영상 축사(#s/07/play) 자동 재생용. 이 플래그 없이 열었다면 송출 전 화면을 한 번 클릭해 두면 됩니다.
- `?clean=1` : 좌하단 화면 ID·영상 진행 바 숨김 (송출용)
- `?t=11:05` : 리허설용 가짜 시각 (프로그램 NOW·카운트다운·NEXT UP 확인)
- `?console=1` : 운영자 콘솔 창. 같은 PC에서 송출 창과 별도로 열면 콘솔에서 클릭한 화면이 송출 창에 반영됩니다 (BroadcastChannel). 콘솔은 노트북 화면, 송출 창은 DID로 보내는 "확장 모드"를 권장합니다.

## 단축키

| 키 | 동작 |
|---|---|
| → / Space / PgDn | 다음 화면 (큐시트 순) · 영상 화면에서 Space는 재생/일시정지 |
| ← / PgUp | 이전 화면 |
| 0 | 대기화면 (60초 자동 순환: 대기→행사안내→프로그램→경품→에티켓) |
| 1~7 | 1 행사안내 · 2 프로그램 · 3 경품 · 4 시작안내 · 5 재개안내 · 6 에티켓 · 7 오찬 |
| 8 / 9 | 8 경품 추첨 카드(4등부터) / 9 폐회 |
| S + 두 자리 | 섹션 간지 직접 이동 (S 0 7 → 영상 축사, S 1 3 → 최백준 대표) |
| F | 전체화면 |
| O / H | 전체 목차 오버레이 (화면 그리드, 클릭 이동) |
| B | 블랙아웃 |
| R | 영상 처음부터 (영상 화면에서만) |
| T | 시계 숨김/표시 |

## 큐시트 (→ 키 순서)

idle → etiquette → start(10:50 카운트다운) → s/01 개회사 → s/02 → s/03 → s/04 → lunch → resume(13:00 카운트다운) → s/06 환영사 → s/07 영상축사 안내 간지 → s/07/play 영상 재생 → s/08 → s/09 → s/10 → s/11/1 → s/11/2 → s/11/3 (축전 3페이지) → s/12 → s/13 → s/14 → s/15 → s/16 추첨안내 → prize/4 → prize/3 → prize/2 → prize/1 → s/16/end 폐회

URL 해시로 직접 진입 가능: `index.html#s/13`, `index.html#prize/1`

## 당일 수정 (index.html 상단 `const DATA`)

- 프로그램·시간: `DATA.program`
- 간지 발표자·제목: `DATA.sessions` (`org`를 비우면 소속 줄이 표시되지 않음 — 틸론소프트 소속은 비워 둠)
- 축전 본문: `DATA.sessions` id "11"의 `pages` (3페이지 배열, `**…**`는 앰버 강조)
- 경품: `DATA.prizes`
- 에티켓 문구: `DATA.etiquette`
- 카운트다운 목표 시각: `DATA.start.target`, `DATA.resume.target`
- 자동 순환 간격·오찬 후 자동 재개: `DATA.settings`

## 에셋

```
assets/
  fonts/PretendardVariable.woff2
  logo/   tilonsoft_w, jaiia_w, gh2_w, jejunu_w (화이트)
  prize/  laptop, watch, tablet, earbuds, qr
  photo/  jin_01~03.jpg (축전 화면 사진 루프)
  video/  kimhankyu_congrats.mp4 (영상 축사)
  bg/     still_main.jpg (정지 배경, 영상 로드 실패 시 폴백)
          loop_main.mp4  (일반 화면 배경 루프, 1920×1080 8.5s, Higgsfield Kling 3.0 → ByteDance 1080p 업스케일, ffmpeg 크로스페이드 루프)
          loop_idle.mp4  (대기화면 배경 루프, 동일 규격)
          _720/          (업스케일 전 720p 원본, 저사양 PC용 예비)
  section/ 01_opening ~ 16_closing.jpg (간지 배경 12장, Higgsfield GPT Image, 1920×1080. 07은 08_congrats, 09는 08_congrats 공용)
```

## 현장 체크리스트

- [ ] 송출 PC 해상도 1920×1080, 배율 100%
- [ ] 영상 축사 오디오: PC 라인아웃 → 음향 콘솔, `#s/07`에서 소리 확인
- [ ] `?t=` 없이 열었는지 확인 (실제 시각 기준)
- [ ] F 키 전체화면 후 상·하단 잘림 없는지 확인
- [ ] 09:30 `#idle` 송출 시작
