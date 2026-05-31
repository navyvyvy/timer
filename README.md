# ☕ Roast Timer

커피 로스팅 전용 다중 타이머 웹앱. 팬 소음과 원두 팝핑 소리가 가득한 로스팅 환경에서도 확실하게 타이밍을 인지할 수 있도록 설계된 PWA입니다.

**[→ 바로 사용하기](https://YOUR_NAME.github.io/roast-timer/)**

---

## 주요 기능

### 🔥 예열 타이머
- 설정한 목표 시간(기본 10분)부터 카운트다운
- 목표 도달 시 알람 (화면 점멸 + 소리 + 진동)
- ±1분 / ±30초 / ±10초 실시간 조절

### ⏱ 마스터 로스팅 타이머
- 생두 투입 시점부터 경과 시간 카운트업
- SVG 원형 프로그레스 링 (88% 초과 시 경고 색상)
- `Date.now()` 절대 시간 기반 — 백그라운드 스로틀링 오차 없음

### 🎯 동적 마일스톤 3단계
| 단계 | 기본 시간 | 내용 |
|------|-----------|------|
| 1 | 5분 | 뒤집기 알람 |
| 2 | 10분 | 상태 체크 알람 |
| 3 | 12분 | 로스팅 완료 → 연장 선택 |

- 로스팅 중에도 ±1분 / ±30초 / ±10초 실시간 조절 가능
- 완료된 단계는 버튼 자동 잠금

### 🚨 강제 경고 알람
- 화면 전체 붉은 점멸 (`@keyframes`)
- 전면 차단 모달 (직접 확인 버튼 누르기 전까지 유지)
- 고음 알람 사운드 반복 재생 (`Web Audio API`)
- 하드웨어 진동 (`navigator.vibrate`)
- **알람 큐 내장** — 여러 마일스톤이 동시에 도달해도 순서대로 표시

### 🔄 로스팅 완료 연장
마지막 마일스톤 도달 시 단순 알람 대신 연장 선택 팝업:
`+3분` / `+4분` / `+5분` / `+6분` 또는 쿨링 진입

---

## 기술 스택

- **순수 HTML/CSS/JS** — 빌드 도구 없음, 의존성 없음
- **Web Audio API** — 소리 생성 (외부 오디오 파일 불필요)
- **Screen Wake Lock API** — 로스팅 중 화면 자동 꺼짐 방지
- **requestAnimationFrame** — 단일 통합 루프로 두 타이머 동시 구동
- **PWA** — 아이폰 홈 화면 추가 시 앱처럼 실행

---

## 설치 및 배포

### GitHub Pages (권장)

```bash
# 1. 리포지토리 생성 및 파일 추가
git init roast-timer
cd roast-timer
cp /path/to/index.html .
git add index.html
git commit -m "feat: initial coffee roasting timer"

# 2. GitHub에 push
git remote add origin https://github.com/YOUR_NAME/roast-timer.git
git push -u origin main
```

GitHub 리포 → **Settings → Pages → Source: main / (root) → Save**

배포 후 `https://YOUR_NAME.github.io/roast-timer/` 접속.

### 아이폰 PWA 설치

1. Safari에서 위 URL 접속
2. 하단 공유 버튼 → **"홈 화면에 추가"**
3. 앱처럼 전체 화면으로 실행됨

---

## 화면 유지 (Wake Lock) 지원 현황

| 환경 | 지원 여부 |
|------|-----------|
| Android Chrome | ✅ 완전 지원 |
| 아이폰 Safari | ❌ 미지원 |
| 아이폰 PWA (홈 화면 추가) | ✅ 대부분 지원 |

> Wake Lock이 미지원인 환경에서는 화면이 꺼지지 않도록 폰 설정에서 자동 잠금 시간을 늘려두세요.

---

## DEV 모드

하단 `DEV` 버튼으로 알람 미리보기 패널 ON/OFF.
로스팅 시작 없이 각 알람의 화면 점멸 · 소리 · 진동을 테스트할 수 있습니다.

---

## 라이선스

MIT
