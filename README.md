# others

지금 쓰는 도구/모델 말고 같은 용도의 **대안을 추천**해 주는 Claude Code 스킬입니다.

코드나 파일 경로를 주면 무엇을 쓰고 있는지 파악하고, 웹 검색으로 최신 대안을 찾아 **공식 문서 링크가 붙은 비교표**로 정리합니다. 파일은 수정하지 않고 추천만 합니다.

## 이런 걸 해 줘요

- 쓰고 있는 것의 이름과 용도를 한 줄로 파악
- 웹 검색으로 대안 3~5개를 찾아 비교표 작성 (이름 / 특징 / 나은 점 / 못한 점 / 난이도 / 공식 문서)
- 상황별 추천과 "가장 먼저 시도해볼 것" 하나 제안
- 공식 문서를 못 찾은 대안은 "공식 문서 미확인"으로 표시, 검색이 안 되면 "미확인, 기억 기준"으로 표시

## 설치

Claude Code 입력창에 **한 줄씩** 입력합니다.

```
/plugin marketplace add 4288-yerim/other-skill
/plugin install others@other-skill
```

두 번째 명령을 치면 설치 범위를 고르는 패널이 열립니다. 어디서나 쓰려면 **Install for you (user scope)** 를 고르세요. 설치가 끝나면 `/reload-plugins`를 한 번 실행합니다.

### 업데이트

레포가 바뀌어도 자동으로 받아지지 않습니다.

```
/plugin marketplace update other-skill
/reload-plugins
```

### 삭제

```
/plugin marketplace remove other-skill
```

마켓플레이스와 그 안에서 설치한 `others`가 함께 지워집니다.

## 사용법

`/others:others` 뒤에 코드, 파일 경로, 또는 말로 설명한 내용을 붙입니다. 플러그인으로 설치하면 이름이 `/플러그인명:스킬명` 형태로 나옵니다.

```
/others:others @경로/ocr_paddle.py
/others:others YOLO로 사람 탐지했어
/others:others 보고서를 개조식으로 씀
```

- 입력이 없으면 "무엇을 쓰고 있는지 알려주세요"라고만 답합니다.
- 사용자가 직접 호출할 때만 동작합니다 (Claude가 알아서 실행하지 않음).

## 실행 결과 예시

PaddleOCR로 번호판을 읽는 코드를 넣었을 때의 결과입니다. (표는 요약본이며, 실제 결과는 검색 시점에 따라 달라집니다.)

```
/others:others @ocr_paddle.py
```

**지금 쓰는 것:** PaddleOCR 3.x(`lang="korean"`)로 번호판 이미지의 글자를 읽는 코드

| 이름 | 한 줄 특징 | 지금 것보다 나은 점 | 못한 점 | 난이도 | 공식 문서 |
|---|---|---|---|---|---|
| RapidOCR | PaddleOCR 모델을 ONNX로 돌리는 경량 툴킷 | `paddlepaddle` 설치 문제를 피할 가능성 | 문서가 주로 중국어 | 쉬움 | https://cdn.jsdelivr.net/gh/rapidai/rapidocr@main/README.md |
| EasyOCR | PyTorch 기반 다국어 OCR | 한글+영어를 간단한 API로 인식 | 번호판 정확도는 직접 비교 필요 | 쉬움 | https://pypi.org/project/easyocr/1.2 |
| Tesseract | 오래된 오픈소스 OCR 엔진 | 설치가 가볍고 CPU만으로 동작 | 번호판 같은 짧은 글자에 약할 것으로 예상 | 중간 | https://packages.debian.org/sk/tesseract-ocr-kor |
| Google Cloud Vision | 클라우드 API | 로컬 설치 문제 없음 | 비용, 인터넷 필요 | 중간 | https://cloud.google.com/vision/pricing?hl=hu |

**상황별 추천:** 설치 문제만 피하려면 RapidOCR, 빠르게 비교하려면 EasyOCR, 안정성이 우선이면 Google Cloud Vision.

**먼저 시도할 것:** RapidOCR. 같은 PaddleOCR 모델을 쓰므로 현재 결과와 바로 비교할 수 있습니다.

마지막에는 참고한 출처 링크(Sources)가 함께 붙습니다.

## 구조

```
.claude-plugin/marketplace.json   # 마켓플레이스 (other-skill)
.claude-plugin/plugin.json        # 플러그인 (others)
skills/others/SKILL.md            # 스킬 본문
```
