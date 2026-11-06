# CameraBook — 인터랙티브 카메라 교과서

빛을 숫자로 바꾸는 기계. 1부에서는 카메라를 렌즈 광학계·구동부·센서·처리 엔진·제어 루프·전원과 열로 분해해 시스템으로 이해하고, 2부에서는 조리개·셔터·ISO부터 초점, 화이트 밸런스, RAW, 플래시, 동영상, 스마트폰 카메라까지 가상 카메라를 직접 조작하며 배우는 한국어 학습 사이트입니다.
1·2부 25개 장, 91개의 시뮬레이터(3D 모델 2개 포함), 용어 253개, 종합 퀴즈와 미션형 촬영 연습장으로 구성됩니다.

자매 사이트: [SensorBook — 이미지 센서 교과서](https://semi.euiyun.com/sensor/) · [PhoneBook — 스마트폰 해부 교과서](../phone/) · [Mobile Image Sensor DB](https://sensors.euiyun.com/)

## 실행
빌드 과정이 없는 정적 사이트입니다.

```bash
python3 -m http.server 8000   # → http://localhost:8000
```
`index.html`을 브라우저로 바로 열어도 동작합니다. KaTeX와 웹 폰트는 CDN에서 불러오며, 없으면 시스템 글꼴로 표시됩니다.

## 구성
| 장 | 파일 | 주제 |
|---|---|---|
| **1부** | | **카메라라는 시스템** |
| 01 | chapters/overview.html | 빛을 숫자로 바꾸는 기계, 짧은 역사, 여섯 하위 시스템(3D 투시 카메라), 광자 예산, 카메라 형식, 제원표 |
| 02 | chapters/anatomy.html | 미러리스 바디·렌즈 3D 분해와 조립, 무게·부피 예산, 플랜지 백 공차 |
| 03 | chapters/optics.html | 광선 추적, 자이델 수차와 색수차, 비구면·ED·코팅, MTF와 회절 한계, 마운트 |
| 04 | chapters/mechanism.html | 포컬 플레인 셔터와 동조 속도, 미러 박스, 조리개 유닛, AF 모터, IBIS 액추에이터 |
| 05 | chapters/sensor.html | 픽셀·풀웰·변환 이득, 베이어 배열, 행 단위 판독과 롤링 셔터, 데이터 대역폭 |
| 06 | chapters/engine.html | ISP 파이프라인, 버퍼와 메모리 카드, 동영상 코덱과 비트레이트 |
| 07 | chapters/control.html | AE·AF·AWB 피드백 루프, 예측 AF와 피사체 추적, 셔터 랙과 EVF 지연 |
| 08 | chapters/body.html | 배터리와 CIPA 매수, 과열의 열 RC 모델, 소재·방진방적, 설계 플레이그라운드 |
| **2부** | | **카메라 다루기** |
| 09 | chapters/basics.html | 바늘구멍 사진기 vs 렌즈, 카메라의 다섯 부품, DSLR·미러리스·폰의 빛 경로, 센서 크기, 화소 수 |
| 10 | chapters/exposure.html | 빛 양동이, 스톱과 EV, 노출 삼각형 가상 카메라, 등가 노출, 써니 16 |
| 11 | chapters/aperture.html | F값과 조리개 날개, 피사계 심도, 보케 모양, 회절과 최적 조리개, 등가 조리개 |
| 12 | chapters/shutter.html | 모션 블러와 패닝, 손떨림, 장노출 빛 궤적, 포컬 플레인 셔터, 롤링 셔터 |
| 13 | chapters/iso.html | ISO = 증폭, 광자 샷 노이즈, ISO 불변성, 센서 크기와 노이즈 감소, Auto ISO |
| 14 | chapters/modes.html | P·A·S·M 모드 다이얼, 18% 회색과 측광 모드, 노출 보정, AE 잠금 |
| 15 | chapters/histogram.html | 라이브 히스토그램과 제브라, 다이내믹 레인지 창문, 브라케팅과 HDR 합성 |
| 16 | chapters/focus.html | MF와 포커스 피킹, 콘트라스트 vs 위상차 AF, AF-S/AF-C, AF 영역 모드 |
| 17 | chapters/focal.html | 화각과 크롭, 돌리 줌(압축 효과의 원인), 셀카 얼굴 비율, 렌즈 왜곡 |
| 18 | chapters/color.html | 색온도, 화이트 밸런스 실험실(회색 카드), 혼합광, 픽처 스타일 |
| 19 | chapters/raw.html | 카메라 내부 현상, 비트 심도와 밴딩, 하이라이트 복구, JPEG 압축(8×8 DCT) |
| 20 | chapters/stabilization.html | OIS·IBIS, 보정 스톱과 성공률, 연사 버퍼, 프리 캡처, 타임랩스 계산 |
| 21 | chapters/flash.html | 광원 크기와 방향, 역제곱 법칙, 가이드 넘버, 동조 속도·HSS, 후막 동조, 필 플래시 |
| 22 | chapters/video.html | 프레임 레이트와 슬로 모션, 180° 셔터, ND 계산, 비트레이트, Log와 그레이딩 |
| 23 | chapters/smartphone.html | 멀티 카메라 줌, 야간 모드 다중 합성, 인물 모드 깊이 지도, 프로 모드 |
| 24 | chapters/playground.html | 미션형 가상 카메라(6개 미션) |
| 25 | chapters/glossary.html | 용어집(253개), 종합 퀴즈(24문항) |

공통 코드: `css/style.css`(디자인 토큰, 라이트/다크), `js/common.js`(내비게이션, 차트·캔버스 헬퍼, 가상 사진 엔진 `CB.Photo`, 원근 투영 렌더러 `CB.World`).
챕터 작성 규칙은 [CONTRIBUTING.md](CONTRIBUTING.md)를 참고하세요.
챕터를 추가하거나 제목·설명을 바꾼 뒤에는 `python3 tools/seo.py`로 canonical/OG/JSON-LD 태그와 `sitemap.xml`을 다시 만듭니다.

시뮬레이터의 사진과 수치는 원리를 보여 주기 위한 교육용 근사 모델입니다.

## 배포
SystemBooks 저장소의 워크플로가 서가 전체와 함께 `https://system.euiyun.com/camera/`로 배포합니다. 2026-11-06에 `geniuskey/camerabook`(`84e2470`)에서 가져왔고, 지금은 이 저장소가 원본입니다.

## 용어집과 본문 뜻풀이

용어 정의는 `js/glossary-data.js`의 `window.BOOK_GLOSSARY`에 저장합니다. 용어집과 본문 뜻풀이가 같은 데이터를 사용하며, 본문에서 용어에 마우스를 올리거나 키보드로 포커스하거나 모바일에서 탭하면 정의를 확인할 수 있습니다. 공통 동작과 스타일은 `js/glossary-tooltips.js`, `css/glossary-tooltips.css`입니다. 데이터 형식은 시리즈 공통 v1이며, 각 항목은 `ko`(이름), `en`(영문명), `abbr`(약어), `def`(정의), `chapters`(관련 장 목록)를 갖습니다. 이름이 반복되면 한 번만 표시하고, 묶음 항목은 가리킨 이름을 제목에 표시하며 구분에 필요한 비교 설명을 함께 제공합니다.

## 라이선스

코드는 [MIT](LICENSE-MIT), 교재 콘텐츠는 [CC BY 4.0](LICENSE-CC-BY-4.0)으로 제공됩니다. 적용 범위와 재사용 조건은 [라이선스 안내](LICENSE.md)를 참고하세요.
