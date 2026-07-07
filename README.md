# 神奈川沖浪裏 — Interactive Portfolio Hero

호쿠사이의 우키요에 「가나가와 해변의 높은 파도」가 마우스(또는 웹캠 손 추적)를 따라
출렁이는 인터랙티브 포트폴리오 히어로 페이지입니다.

원본 판화의 픽셀을 WebGL 셰이더로 **변위(displacement)만** 시키기 때문에
화풍과 색감은 단 한 픽셀도 바뀌지 않습니다.

## 실행

정적 파일이라 서버에 올리기만 하면 됩니다. 로컬 확인:

```bash
python3 -m http.server 8000
# http://localhost:8000 접속
```

GitHub Pages에 배포하면 그대로 동작합니다 (Settings → Pages → 브랜치 선택).

## 인터랙션

| 입력 | 효과 |
|---|---|
| 마우스 이동 | 움직인 방향으로 파도가 솟구치고 잔물결이 퍼짐 |
| 클릭 / 터치 | 그 지점에서 물결이 크게 출렁임 |
| ✋ 손 추적 켜기 | 웹캠으로 검지 끝을 추적해 손짓으로 파도를 이끎 (MediaPipe, 전부 브라우저 로컬 처리) |
| 카메라 거부/실패 | 자동으로 마우스 모드 유지 |

가만히 두어도 바다가 은은하게 숨쉬는 상시 잔물결이 있습니다.
하늘과 후지산은 마스크로 고정되어 움직이지 않습니다.

## 파일 구성

- `index.html` — 페이지 전체 (CSS/JS/셰이더 단일 파일, 외부 라이브러리 없음. 손 추적 사용 시에만 MediaPipe를 CDN에서 로드)
- `assets/wave.jpg` — 원본 판화 (워터마크 제거 + EDSR 4배 초해상도, 3292×2104)
- `assets/mask.png` — 파도 영역 마스크 (흰 부분만 움직임)

## 문구 수정

`index.html`의 `.hero-copy` 블록에서 이름/직함/안내 문구를 수정하세요:

```html
<div class="hero-copy">
  <div class="kicker">Interactive Portfolio</div>
  <h1>이름을 입력하세요<br>Creative Developer</h1>
  ...
</div>
```

파도 세기는 `index.html` 셰이더의 `ampMouse`(마우스), `ampSplash`(클릭),
상시 잔물결은 `0.0026` / `0.0014` 계수로 조절합니다.

## 원작

葛飾北斎 (Katsushika Hokusai), 〈神奈川沖浪裏〉, 1831년경 — 퍼블릭 도메인.
