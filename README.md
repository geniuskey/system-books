# SystemBooks · 시스템 교과서 서가

자동차, 선박, 스마트폰, 카메라처럼 수많은 부품이 맞물려 하나로 움직이는 시스템을 3D 모델과 시뮬레이터로 분해하며 배우는 한국어 인터랙티브 교과서를 한 저장소에서 관리합니다. 홈은 SemiBooks·MathBooks의 책장·검색·분야 필터·실습·읽는 순서 구성을 따릅니다.

서비스 주소: **https://system.euiyun.com/** · 책 한 권의 홈은 **`/{slug}/`**, 각 장은 **`/{slug}/chapters/{chapter}.html`**입니다.

## 수록 책

| 경로 | 책 | 상태 | 처음 가져온 곳 |
|---|---|---|---|
| `/car/` | CarBook · 자동차 교과서 | 공개, 21개 장 + 용어집 | `geniuskey/carbook` |
| `/ship/` | ShipBook · 선박 교과서 | 공개, 22개 장 + 용어집 | `geniuskey/shipbook` |
| `/phone/` | PhoneBook · 스마트폰 해부 교과서 | 공개, 13개 장 + 용어집 | `geniuskey/phonebook` |
| `/camera/` | CameraBook · 카메라 교과서 | 공개, 24개 장 + 용어집 | `geniuskey/camerabook` |

준비 중인 책은 `roadmap.json`에 적습니다(지금은 비어 있음). 장 목록은 각 책의 `js/common.js`에, 집필 규칙은 각 책의 `CONTRIBUTING.md`에 있습니다.

## 구성

```text
index.html, shelf.css                  서가 홈: 책장·분야 필터·검색, 대표 실험, 읽는 순서
catalog.js                            생성된 책 목록(직접 수정하지 않음)
book.json                             서가 메타데이터, 각 책의 book.json 목록
roadmap.json                          준비 중인 책
shared/js/shelf.js                    서가 홈의 책장 렌더링·필터
shared/js/covers.js                   SVG 책 표지(books 포털 코드)
shared/css/cover-animations.css       표지 애니메이션, 동작 줄이기 지원
shared/img/sims/                      홈 ‘직접 해보기’의 시뮬레이터 화면
shared/js/book-shell.js               모든 책 상단 바의 ‘시스템 서가’ 연결
{slug}/                               각 책의 본문, 실습 엔진, 용어 데이터, 책별 검사 도구(tools/, scripts/)
tools/sync-catalog.py                 catalog.js 생성(BOOKS + roadmap.json)
tools/sync-sitemap.py                 루트 사이트맵 생성
tools/build.mjs                       정적 배포물(.book-dist/) 생성, canonical 검사와 GA4 태그
tools/check.py                        메타데이터·링크 정적 검사
tools/browser-check.cjs               데스크톱·모바일 브라우저 검사(Playwright)
tools/og.mjs                          서가 공유 이미지 og.png 생성(Playwright)
```

## 실행과 배포

```bash
npm ci
npm test
npm run build
python3 -m http.server 8000 --directory .book-dist
```

`npm test`는 CarBook·ShipBook·PhoneBook의 `scripts/verify-factcheck.cjs`(시뮬레이터 물리 검증)와 `tools/check.py`를 차례로 돌립니다. CameraBook에는 별도 물리 검증 스크립트가 없습니다.

배포물은 `.book-dist/`입니다. GitHub Pages의 Source를 GitHub Actions로 설정하고 커스텀 도메인 `system.euiyun.com`과 DNS를 연결합니다. `main`에 push하거나 Deploy Book 워크플로를 실행하면 검사·빌드 후 배포합니다. 이 저장소의 CNAME 설정만으로 DNS나 GitHub 설정이 자동으로 바뀌지는 않습니다.

네 책은 가져올 때의 canonical·Open Graph 태그와 CDN 의존성(KaTeX·three.js·폰트)을 그대로 씁니다. 분석 태그는 소스에 두지 않고 빌드가 페이지마다 한 번 붙입니다. 새 장을 쓸 때는 기존 장처럼 `</head>` 바로 앞에 `shared/css/book-shell.css`와 `shared/js/book-shell.js`를 연결합니다. 책의 `tools/seo.py`를 다시 돌리면 이 서가 주소(`https://system.euiyun.com/{slug}/`)로 태그를 만듭니다.

책·장·시뮬레이터 수가 바뀌면 `npm run catalog`, `npm run sitemap`, `node tools/og.mjs`로 목록과 공유 이미지를 갱신합니다.

## 가져온 책

네 책은 2026-11-06에 개별 저장소에서 한 번 가져왔고, 지금은 이 저장소가 유일한 원본입니다. 책을 고칠 때는 이 저장소의 파일을 직접 수정합니다. 개별 저장소와 기존 도메인(`*book.euiyun.com`)은 리다이렉트 없이 내립니다. 모든 책은 `system.euiyun.com/{slug}/`에서만 제공합니다.

| 책 | 원본 저장소 | 가져온 커밋 | 기존 주소 |
|---|---|---|---|
| CarBook | `geniuskey/carbook` | `24c3a8d` | `carbook.euiyun.com` |
| ShipBook | `geniuskey/shipbook` | `f8e5d2f` | `shipbook.euiyun.com` |
| PhoneBook | `geniuskey/phonebook` | `6d929cb` | `phonebook.euiyun.com` |
| CameraBook | `geniuskey/camerabook` | `84e2470` | `camerabook.euiyun.com` |

가져올 때 바꾼 것:

- 각 저장소의 추적 파일을 복사하고 `.github/`, `CNAME`, `package.json`, `package-lock.json`, `.gitignore`는 뺐습니다(배포는 이 저장소의 워크플로가 맡음). ShipBook에는 `book.json`이 없어 새로 만들었습니다.
- `https://{carbook,shipbook,phonebook,camerabook}.euiyun.com` → `https://system.euiyun.com/{car,ship,phone,camera}`, `https://sensorbook.euiyun.com` → `https://semi.euiyun.com/sensor`. 본문 링크(`<a href>`)는 같은 호스트의 `/car/…` 같은 경로로 바꿨고 canonical·Open Graph는 절대 주소로 남겼습니다.
- 각 책의 테마 저장 키(CarBook·CameraBook `cb-theme`, ShipBook `sb-theme`, PhoneBook `pb-theme`)를 서가 홈과 같은 `system-theme`으로 통일했습니다.
- 소스에 있던 Cloudflare 비컨과 GA4 태그를 지웠습니다(빌드가 GA4 태그를 붙임).
- 모든 HTML의 `</head>` 앞에 서가 연결 스크립트(`shared/js/book-shell.js`)를 넣었습니다.
- CameraBook은 가져온 뒤 카메라를 시스템으로 분해하는 1부(1~8장: 전체 그림, 해부, 렌즈 광학계, 구동부, 센서, 처리 엔진, 3A 제어, 전원·열·바디)를 새로 쓰고, 기존 17개 장을 2부(9~25장)로 옮겼습니다. 본문의 장 번호 참조와 그림 번호도 함께 고쳤습니다. 촬영 연습장의 저장 키는 `camera-play`로 바꿨습니다.

## 새 책 추가

책마다 `{slug}/index.html`, `{slug}/chapters/`, `{slug}/book.json`을 두고 루트 `book.json`의 `books`에 등록합니다. 서가 메타데이터는 `tools/sync-catalog.py`의 `BOOKS`에 추가합니다. 공개할 때 `roadmap.json`의 예정 항목을 지우고 `npm run catalog`와 `npm run sitemap`을 실행합니다.

## 라이선스

코드는 MIT, 교육 콘텐츠는 CC BY 4.0입니다. [라이선스 안내](LICENSE.md)와 각 책의 저작권 표시를 참고하세요.
