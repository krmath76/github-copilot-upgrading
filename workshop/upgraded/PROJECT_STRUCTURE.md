# Guachi 프로젝트 구조 설명

## 프로젝트 개요
Guachi는 Python 2.5 시대에 개발된 레거시 구성 관리 라이브러리로, 전역적으로 접근 가능한 영속적 딕셔너리 구성을 제공합니다. INI 스타일 키를 딕셔너리 키로 매핑하고 누락된 값에 대한 기본값을 자동으로 채워줍니다.

## 디렉토리 구조

```
upgraded/
├── .keep                          # Git에서 빈 폴더 추적용 파일
├── MANIFEST.in                    # 패키지에 포함할 추가 파일 정의
├── README.rst                     # 프로젝트 설명 문서 (reStructuredText 형식)
├── distribute-0.6.10.tar.gz       # 레거시 distribute 패키지 (Python 2 시대)
├── distribute_setup.py            # distribute 설정 스크립트 (deprecated)
├── setup.py                       # 패키지 설치 및 배포 설정 파일
├── docs/                          # 문서 디렉토리
│   ├── Makefile                   # Sphinx 문서 빌드용 Makefile
│   ├── build/                     # 빌드된 문서 출력 디렉토리
│   │   ├── doctrees/              # Sphinx doctree 캐시 파일들
│   │   └── html/                  # HTML 형식으로 빌드된 문서
│   │       ├── _sources/          # 원본 소스 파일들 (txt 형식)
│   │       ├── _static/           # CSS, JS, 이미지 등 정적 파일들
│   │       └── *.html             # 생성된 HTML 문서 페이지들
│   └── source/                    # Sphinx 소스 문서 디렉토리
│       ├── _static/               # 사용자 정의 정적 파일들
│       ├── conf.py                # Sphinx 구성 파일
│       └── *.rst                  # reStructuredText 형식 문서들
├── guachi/                        # 메인 패키지 디렉토리
│   ├── __init__.py                # 패키지 초기화 및 ConfigMapper 클래스
│   ├── config.py                  # 구성 매핑 관련 기능
│   ├── database.py                # 데이터베이스 관련 기능 (영속성)
│   └── tests/                     # 테스트 디렉토리
│       ├── test_configmapper.py   # ConfigMapper 클래스 테스트
│       ├── test_configurations.py # 구성 관련 테스트
│       ├── test_database.py       # 데이터베이스 기능 테스트
│       └── test_integration.py    # 통합 테스트
└── guachi.egg-info/               # setuptools가 생성한 메타데이터
    ├── PKG-INFO                   # 패키지 정보
    ├── SOURCES.txt                # 소스 파일 목록
    ├── dependency_links.txt       # 의존성 링크
    └── top_level.txt              # 최상위 모듈 목록
```

## 주요 파일 설명

### 핵심 파일들

- **`setup.py`**: Python 2.5-2.7을 지원하는 레거시 패키지 설정 파일
  - `distribute_setup`을 사용 (현재는 `setuptools`로 통합됨)
  - MIT 라이선스
  - Google Code 호스팅 (현재는 사용되지 않음)

- **`guachi/__init__.py`**: 메인 `ConfigMapper` 클래스 정의
  - INI 파일을 딕셔너리로 변환
  - 영속적 저장소 관리
  - 기본값 설정 및 관리

### 레거시 요소들

1. **Python 2.x 특화 코드**:
   - `distribute_setup.py` 사용
   - Python 2.5-2.7 분류자
   - 구식 `print` 문법 가능성

2. **사용 중단된 도구들**:
   - `distribute` 패키지 (현재는 `setuptools`로 통합)
   - Google Code 호스팅
   - 구식 Sphinx 문서 구조

3. **호환성 문제 가능성**:
   - 예외 처리 문법
   - `import` 문 구조
   - 문자열 처리 방식

## 업그레이드 필요 사항

이 프로젝트를 Python 3.x로 업그레이드하려면 다음 사항들을 고려해야 합니다:

1. **setup.py 현대화**:
   - `distribute_setup` 제거
   - `setuptools` 직접 사용
   - Python 3.x 분류자 추가

2. **코드 마이그레이션**:
   - `print` 문을 `print()` 함수로 변경
   - 예외 처리 문법 업데이트
   - 상대/절대 import 정리

3. **의존성 업데이트**:
   - 최신 `setuptools` 사용
   - 테스트 프레임워크 현대화
   - 문서 도구 업데이트

4. **호스팅 및 메타데이터**:
   - GitHub로 호스팅 이전
   - URL 및 이메일 주소 업데이트
   - 라이선스 파일 추가

## 테스트 전략

업그레이드 과정에서 기존 기능의 정확성을 보장하기 위해:

1. 현재 테스트 스위트 실행 및 검증
2. Python 3.x 호환성 테스트 추가
3. 통합 테스트를 통한 전체 워크플로우 검증
4. 성능 회귀 테스트

이 구조는 전형적인 Python 2.x 시대 프로젝트의 특징을 잘 보여주며, GitHub Copilot을 활용한 체계적인 업그레이드 과정의 좋은 예시가 될 것입니다.