# ai-programming-test

## ① 무엇을 하나요 (What)

CSV 파일에서 학생 이름과 점수를 읽어 유효한 성적 데이터를 추출하고, 잘못된 행은 제외하는 프로그램입니다.

## ② 왜 만들었나요 (Why)

실제 CSV 파일에는 빈 칸, 점수 범위 밖의 값, 중복 이름 등 다양한 예외 상황이 발생할 수 있습니다. 이러한 데이터를 안전하게 처리하는 프로그램을 작성하고, 직접 작성한 테스트와 AI가 생성한 테스트를 비교하여 정상·예외·경계값 검사의 차이를 확인하고자 했습니다. 또한 AI가 기존 코드의 버그를 발견하는지도 실험했습니다.

## ③ 어떻게 쓰나요 (How)

Python이 설치된 환경에서 아래 명령어를 실행합니다.

```bash
# 설치
python -m pip install pytest pytest-cov

# 실행 및 테스트
python -m pytest test_load_scores.py -v
```

## ④ 어떻게 테스트하나요

```bash
# 직접 작성한 테스트
python -m pytest test_load_scores.py -v --cov=load_scores --cov-report=term-missing

# AI A 테스트
python -m pytest test_ai_A.py -v --cov=load_scores --cov-report=term-missing

# AI B 테스트
python -m pytest test_ai_B.py -v --cov=load_scores --cov-report=term-missing

# 별도 버그 검출 테스트
python -m pytest test_bugs.py -v
```

실행 결과:

| 테스트 | 결과 | 커버리지 |
| --- | --- | --- |
| 직접 작성 | 9 passed | 76% |
| AI A (코드 제공) | 8 passed | 80% |
| AI B (명세 제공) | 13 passed, 1 failed | 80% |
| 별도 버그 검출 | 1 passed, 1 failed | - |

AI B와 별도 버그 검출 테스트에서 발생한 실패는 `find_max()`가 마지막 원소를 검사하지 않는 버그를 발견한 결과입니다. 버그 자체는 수정하지 않았습니다.

## ⑤ 파일 구성

| 파일 | 하는 일 |
| --- | --- |
| `load_scores.py` | CSV 성적 데이터를 읽고 처리하는 프로그램 |
| `test_load_scores.py` | 직접 작성한 테스트 코드 |
| `test_ai_A.py` | 소스 코드를 제공하여 AI가 생성한 테스트 |
| `test_ai_B.py` | 함수 명세를 제공하여 AI가 생성한 테스트 |
| `bug3_logic.py` | 마지막 원소를 검사하지 않는 버그가 포함된 코드 |
| `test_bugs.py` | AI가 생성한 버그 검출 테스트 |
| `*.csv` | 성적 데이터 및 예외 상황 검사용 파일 |

## ⑥ 만든 사람 · AI를 어디에 썼는지

- 만든 사람 : 강지안 / 2026100735
- AI를 쓴 곳 : `load_scores()`의 테스트 코드 생성과 `find_max()`의 버그 검출 테스트 작성에 활용했습니다.
- 내가 직접 판단한 것 : 테스트 결과와 커버리지를 비교하고, 실패 원인이 테스트 코드의 오류인지 기존 프로그램의 버그인지 확인했습니다.

## 라이선스

MIT License (LICENSE 파일 참고)

