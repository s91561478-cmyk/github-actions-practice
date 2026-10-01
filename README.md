# GitHub Actions Practice

GitHub Actions를 이용한 CI/CD 학습 및 실습을 기록하기 위한 Repository입니다.

## 1. 실습 내용

GitHub Actions의 기본적인 Workflow를 작성하고 GitHub Repository에 Push하여
Workflow가 실행되는 과정을 확인했습니다.

### 학습 내용

- `.github/workflows/` 디렉터리에 Workflow 작성
- `push` 이벤트를 이용한 Workflow 실행
- `ubuntu-latest` GitHub-hosted Runner 사용
- 여러 개의 Step 실행
- 여러 줄의 명령어 실행
- GitHub Actions 환경 변수 사용
  - `GITHUB_SHA`
  - `GITHUB_REPOSITORY`
- GitHub Actions Secrets 사용

### Workflow 실행 흐름

```text
Git Push
   ↓
Push 이벤트 발생
   ↓
Workflow 실행
   ↓
Runner 할당
   ↓
Set up job
   ↓
Steps 실행
   ↓
Complete job
   ↓
Workflow 완료
```

## 2. 트러블슈팅

### 1) Workflow 문법 오류

**문제**

Workflow 실행 시 다음과 같은 오류가 발생했습니다.

```text
Invalid workflow file
Unexpected value 'Name'
Unexpected value 'On'
```

**원인**

GitHub Actions의 키를 `Name`, `On`으로 잘못 작성했습니다.

**해결**

GitHub Actions의 올바른 키인 `name`, `on`으로 수정하여 문제를 해결했습니다.

```yaml
name: github-actions-test

on:
  push:
    branches:
      - main
```

---

### 2) Runner 할당 대기 문제

**문제**

Job이 `Queued` 상태에서 계속 대기하며 다음과 같은 메시지가 출력되었습니다.

```text
Requested labels: ubutu-latest
Waiting for a runner to pick up this job...
```

**원인**

`runs-on`에 지정한 Ubuntu Runner Label에 오타가 있었습니다.

```yaml
runs-on: ubutu-latest
```

**해결**

Runner Label을 `ubuntu-latest`로 수정한 후 정상적으로 Runner가 할당되어 Job 실행에 성공했습니다.

```yaml
runs-on: ubuntu-latest
```

## 3. 배운 점

- GitHub Actions의 Workflow는 `.github/workflows/` 디렉터리에 YAML 파일로 작성한다.
- Workflow는 `Workflow → Job → Step` 구조로 구성된다.
- `on`을 통해 Push 등의 이벤트를 감지하여 Workflow를 자동으로 실행할 수 있다.
- `runs-on`을 통해 Job을 실행할 Runner 환경을 지정할 수 있다.
- GitHub-hosted Runner를 사용하면 별도의 실행 서버를 직접 구축하지 않아도 된다.
- Job 실행 시 `Set up job → Steps 실행 → Complete job` 순서로 진행된다.
- 환경 변수와 Secrets를 활용하여 Workflow에서 필요한 값을 사용할 수 있다.
- 오류 발생 시 Workflow 실행 로그를 확인하여 문법, Runner Label 등의 설정을 확인하는 것이 중요하다.

## 4. 학습 기록

GitHub Actions 및 CI/CD에 대해 학습한 이론 내용은 개인 블로그에 정리했습니다.

- [GitHub Actions 및 CI/CD 학습 정리 - Naver Blog](https://blog.naver.com/siksikhanjapenlife/224427921410)