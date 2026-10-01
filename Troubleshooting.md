1.Workflow 문법 오류
■ 문제상황
GitHub Actions의 Workflow 파일을 작성하여 GitHub 레지스토리에 Push 했지만 Workflow가 실행되지 않고 오류가 발생

Invalid workflow file

(Line: 1, Col: 1): Unexpected value 'Name'
(Line: 2, Col: 1): Unexpected value 'On'

■ 원인
GitHub Actions Workflow의 키는 대소문자를 구분한다.
Workflow 파일에서 Name과 On의 앞글자를 대문자로 작성하였다.

Name: github-actions-test

On:
  push:
    branches:
      - main

■ 대책
Name, On을 소문자로 수정

name: github-actions-test

on:
  push:
    branches:
      - main

■ 배운점
GitHub Actions의 Workflow에서는 name, on, jobs, steps, runs-on 등 정해진 키의 대소문자를 정확하게 작성해야 한다.


2.Runner 할당 대기 문제
■ 문제상황
GitHub Actions Workflow를 작성하고 GitHub Repository에 Push했지만, Job이 실행되지 않고 오랫동안 Queued 상태로 대기했다.
Job의 실행 로그를 확인한 결과 다음과 같은 메시지가 출력되었다.

Requested labels: ubutu-latest
Waiting for a runner to pick up this job...

■ 원인
Workflow의 runs-on에 지정한 Ubuntu Runner의 이름에 오타가 있었다.

jobs:
  My-Deploy-Job:
    runs-on: ubutu-latest

■ 대책
runs-on에 지정한 Runner Label의 오타를 수정

jobs:
  My-Deploy-Job:
    runs-on: ubuntu-latest

■ 배운점
GitHub Actions가 Waiting for a runner to pick up this job... 상태에서 비정상적으로 오래 대기한다면 GitHub 장애만 의심하기보다 먼저 runs-on에 지정한 ubuntu-latest, windows-latest 등의 Runner Label이 정확한지 확인한다.