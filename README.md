# AI Build Harness

이 저장소는 일반적인 코딩 업무 전반을 지원하기 위한 AI 코딩 하네스입니다.

대상 업무:

- 기능 구현
- 버그 수정
- 테스트 작성
- 디버깅
- 코드 리뷰
- 문서화
- 릴리즈 준비

핵심 구현은 `.github/` 아래에 모여 있으며, GitHub Copilot 같은 코딩 에이전트가 저장소 안에서 일관된 방식으로 동작하도록 돕습니다.

## 이 하네스가 하는 일

이 하네스는 크게 세 가지 축으로 구성됩니다.

- 훅: 에이전트 세션 중 자동으로 실행되는 작업
- 스킬: 일반적인 코딩 업무를 잘게 나눈 작업 지침서
- 에이전트: 특정 역할을 맡는 전용 에이전트 정의 영역

즉, 단순히 훅만 있는 저장소가 아니라, 일반 개발 흐름 전체를 보조하는 작업용 베이스라고 보면 됩니다.

## 저장소 구조

실제 핵심 내용은 아래 경로에 있습니다.

- `.github/hooks/`: 크로스플랫폼 훅 런타임
- `.github/skills/`: 코딩 업무용 스킬 문서 모음
- `.github/agents/`: 전용 에이전트 정의 영역
- `.github/logs/`: 훅 실행 중 생성되는 로컬 로그

세부 설명은 `.github/README.md`에 정리되어 있습니다.

## 필수 설치

필수:

- `git`
- `node`

권장:

- Node.js 20 이상

선택:

- `prettier`: JS/TS/JSON/YAML/Markdown/CSS/HTML 포맷팅
- `ruff`: Python 린트/포맷팅

선택 도구가 없어도 하네스는 동작합니다. 다만 관련 포맷/린트 단계는 건너뛰고, 설치 방법은 로그에 남깁니다.

## 운영체제별 설치

### macOS

```bash
brew install git node
```

선택 도구:

```bash
npm install --global prettier
python3 -m pip install ruff
```

### Windows

```powershell
winget install --id Git.Git -e
winget install --id OpenJS.NodeJS.LTS -e
```

선택 도구:

```powershell
npm install --global prettier
py -m pip install ruff
```

`winget`이 없으면 공식 설치 프로그램이나 Chocolatey를 사용해도 됩니다.

### Linux

Debian/Ubuntu 예시:

```bash
sudo apt-get update
sudo apt-get install -y git nodejs npm
```

선택 도구:

```bash
npm install --global prettier
python3 -m pip install ruff
```

Fedora/RHEL 계열은 `apt-get` 대신 `dnf`를 사용하면 됩니다.

## 훅 실행 요건

활성 훅 설정은 `.github/hooks/hooks.json`에 있고, 실제 실행기는 `.github/hooks/hook-runner.mjs`입니다.

최소 조건:

1. `git`이 설치되어 있어야 합니다.
2. `node`가 `PATH`에 있어야 합니다.
3. Copilot이 저장소 루트 기준으로 훅을 실행할 수 있어야 합니다.

선택 조건:

1. `prettier`를 설치하면 웹/문서 계열 파일 자동 포맷이 동작합니다.
2. `ruff`를 설치하면 Python 파일 자동 린트/포맷이 동작합니다.

## 로그는 커밋하지 않음

훅이 만드는 `.github/logs/`는 로컬 런타임 산출물입니다.

이 경로는 `.gitignore`에 추가되어 있어서 Git에 올라가지 않도록 처리되어 있습니다.

## GitHub 공식 기능과의 관계

GitHub는 `.github/` 아래에서 여러 저장소 설정 파일을 공식적으로 지원합니다. 예를 들면 아래와 같습니다.

- `.github/copilot-instructions.md`
- `.github/instructions/*.instructions.md`
- `CODEOWNERS`
- 워크플로우, 템플릿 등

이 저장소는 그 공식 패턴을 바탕으로, `.github/`를 일반 코딩 업무용 AI 하네스 영역으로 확장해서 사용합니다.

참고 문서:

- GitHub Copilot 저장소 지침: https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions
- GitHub CODEOWNERS: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners