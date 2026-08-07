# E1-1 Linux CLI / Docker / Git 실습

## 프로젝트 소개

Codyssey E1-1 미션입니다.

이번 프로젝트에서는 Linux CLI, 파일 권한(Permission), Docker, Dockerfile, Docker Container, Volume, Docker Compose, Git, GitHub를 직접 실습하며 개발 환경이 어떻게 구성되는지 단계별로 학습하였습니다.

단순히 명령어를 실행하는 것에서 끝나는 것이 아니라, 실제 터미널에서 발생한 오류를 해결하고 Docker가 이미지를 생성하는 과정과 컨테이너가 실행되는 원리까지 직접 확인하는 것을 목표로 하였습니다.

프로젝트 진행 과정에서 발생한 오류와 해결 과정도 함께 기록하여 실습 내용을 최대한 재현할 수 있도록 작성하였습니다.

---

# 목차

1. 프로젝트 목표
2. 개발환경
3. 프로젝트 구조
4. 전체 실습 과정
5. Linux CLI 실습
6. File Permission
7. Docker 설치 및 확인
8. Hello World 실행
9. Dockerfile 작성
10. Docker Image Build
11. Docker Container 실행
12. Docker Volume(Bind Mount)
13. Docker Compose
14. Git & GitHub
15. 느낀점

---

# 1. 프로젝트 목표

이번 프로젝트를 통해 아래 내용을 직접 실습하였습니다.

- Linux CLI 명령어 사용
- 디렉터리 생성 및 이동
- 파일 생성
- Linux 파일 권한 변경
- Docker 설치 및 실행
- Docker Image Build
- Docker Container 실행
- Port Mapping
- Bind Mount
- Docker Compose
- Git Commit
- GitHub Push

또한 단순히 성공한 과정만 기록하지 않고 실습 도중 발생했던 오류와 해결 방법까지 함께 정리하였습니다.

---

# 2. 개발환경

|항목|내용|
|-----|-----|
|OS|Windows 11 + WSL2|
|Terminal|Git Bash|
|IDE|Visual Studio Code|
|Docker|29.6.2|
|Git|Git for Windows|
|Repository|GitHub|

📷 개발환경 스크린샷

---

# 3. 프로젝트 구조

프로젝트 구조는 아래와 같습니다.

```text
codyssey-1
│
├── README.md
│
└── practice
    ├── Dockerfile
    ├── docker-compose.yml
    ├── index.html
    └── test.txt
```

각 파일의 역할은 다음과 같습니다.

|파일|설명|
|-----|------|
|README.md|실습 내용 정리|
|Dockerfile|Docker Image 생성|
|docker-compose.yml|Docker Compose 실행|
|index.html|Nginx에서 출력할 웹 페이지|
|test.txt|Linux CLI 및 Permission 실습용 파일|

📷 프로젝트 구조

---

# 4. 전체 실습 과정

이번 프로젝트는 아래 순서대로 진행하였습니다.

1. 현재 작업 위치 확인
2. practice 디렉터리 생성
3. test.txt 생성
4. 파일 권한 확인
5. chmod를 이용한 권한 변경
6. Docker 설치 확인
7. Docker Engine 확인
8. Hello World 실행
9. Dockerfile 작성
10. Docker Build
11. Docker Container 실행
12. Port Mapping
13. Volume(Bind Mount)
14. Docker Compose
15. Git Commit
16. GitHub Push

---

# 5. Linux CLI 실습

Linux CLI 실습에서는 디렉터리 생성, 이동, 파일 생성, 파일 확인 등을 수행하였습니다.

---

## 5-1 현재 작업 위치 확인

먼저 현재 작업 중인 디렉터리를 확인하였습니다.

### 실행 명령

```bash
pwd
```

### 실제 터미널 출력

```text
$ pwd

/c/Users/jkhlm/codyssey-1
```

현재 프로젝트가 저장되어 있는 위치를 확인할 수 있었습니다.

Linux에서는 pwd(Print Working Directory) 명령을 사용하여 현재 작업 중인 디렉터리를 확인할 수 있습니다.

📷 pwd 실행 화면

---

## 5-2 practice 디렉터리 생성

Docker 실습을 위한 practice 폴더를 생성하였습니다.

### 실행 명령

```bash
mkdir practice
```

mkdir(make directory)은 새로운 디렉터리를 생성하는 명령어입니다.

실행 후 생성된 practice 디렉터리로 이동하였습니다.

### 실행 명령

```bash
cd practice
```

### 실제 터미널 출력

```text
$ mkdir practice

$ cd practice

jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)
```

Linux에서는 cd(Change Directory)를 이용하여 원하는 디렉터리로 이동할 수 있습니다.

📷 practice 생성 화면

---

## 5-3 test.txt 생성

빈 텍스트 파일을 생성하였습니다.

### 실행 명령

```bash
touch test.txt
```

touch 명령은 새로운 파일을 생성하거나 기존 파일의 수정 시간을 변경하는 명령어입니다.

파일 생성 후 정상적으로 생성되었는지 확인하기 위해 아래 명령을 실행하였습니다.

```bash
ls -la
```

### 실제 터미널 출력

```text
$ touch test.txt

$ ls -la

total 0

drwxr-xr-x 1 jkhlm 197609 0 Aug 5 21:08 ./

drwxr-xr-x 1 jkhlm 197609 0 Aug 5 21:07 ../

-rw-r--r-- 1 jkhlm 197609 0 Aug 5 21:08 test.txt
```

### 출력 결과 분석

출력된 내용을 보면

```
-rw-r--r--
```

형태로 권한이 표시됩니다.

여기서

- 첫 번째 "-"는 일반 파일을 의미합니다.
- rw-는 Owner 권한입니다.
- r--는 Group 권한입니다.
- r--는 Other 권한입니다.

즉,

현재 test.txt는

- Owner : 읽기 / 쓰기 가능
- Group : 읽기만 가능
- Other : 읽기만 가능

상태임을 확인할 수 있었습니다.

📷 touch 실행 화면

---

## 5-4 파일 권한 확인

생성한 파일의 권한을 자세히 확인하기 위해 아래 명령을 실행하였습니다.

### 실행 명령

```bash
ls -l test.txt
```

### 실제 터미널 출력

```text
$ ls -l test.txt

-rw-r--r-- 1 jkhlm 197609 0 Aug 5 21:08 test.txt
```

Linux에서는 ls -l 옵션을 사용하면 파일의 권한, 소유자, 그룹, 파일 크기, 수정 시간 등을 함께 확인할 수 있습니다.

Permission은 이후 chmod 명령을 이용하여 변경할 수 있습니다.

📷 ls -l 실행 화면

---
# 6. File Permission(파일 권한) 실습

Linux에서는 모든 파일과 디렉터리에 대해 접근 권한(Permission)이 존재합니다.

권한은 크게 아래 세 가지로 구성됩니다.

|권한|의미|
|------|------|
|r|Read (읽기)|
|w|Write (쓰기)|
|x|Execute (실행)|

그리고 권한은 아래 세 사용자 그룹에게 각각 부여됩니다.

- Owner (파일 소유자)
- Group (같은 그룹 사용자)
- Other (그 외 사용자)

---

## 6-1 현재 권한 확인

먼저 생성한 test.txt 파일의 권한을 확인하였습니다.

### 실행 명령

```bash
ls -l test.txt
```

### 실제 터미널 출력

```text
$ ls -l test.txt

-rw-r--r-- 1 jkhlm 197609 0 Aug 5 21:08 test.txt
```

현재 권한은

```
rw-r--r--
```

입니다.

이를 숫자로 표현하면

```
644
```

권한과 같습니다.

### 권한 분석

|구분|권한|
|------|------|
|Owner|Read + Write|
|Group|Read|
|Other|Read|

즉,

파일 소유자는 읽기와 쓰기가 가능하지만 실행은 불가능하며,

같은 그룹과 기타 사용자는 읽기만 가능합니다.

📷 권한 확인 스크린샷

---

## 6-2 chmod 명령어 사용

이번에는 chmod(Change Mode)를 이용하여 파일 권한을 변경하였습니다.

### 실행 명령

```bash
chmod 755 test.txt
```

명령 실행 후 다시 권한을 확인하였습니다.

```bash
ls -l test.txt
```

### 실제 터미널 출력

```text
$ chmod 755 test.txt

$ ls -l test.txt

-rwxr-xr-x 1 jkhlm 197609 0 Aug 5 21:08 test.txt
```

권한이

```
rwxr-xr-x
```

로 변경된 것을 확인할 수 있었습니다.

---

### 755의 의미

Linux에서는

- r = 4
- w = 2
- x = 1

값을 더하여 숫자로 표현합니다.

따라서

|숫자|권한|
|------|------|
|7|4+2+1 = rwx|
|5|4+1 = r-x|
|5|4+1 = r-x|

즉

```
755
```

는

```
rwxr-xr-x
```

와 동일한 권한입니다.

Owner는

- Read
- Write
- Execute

권한을 모두 가지며,

Group과 Other는

- Read
- Execute

권한만 갖습니다.

📷 chmod 실행 화면

---

## 이번 실습에서 배운 점

이번 Permission 실습을 통해 Linux에서는 모든 파일에 접근 권한이 존재한다는 것을 확인할 수 있었습니다.

또한 chmod 명령을 이용하여 권한을 숫자로도 변경할 수 있다는 점을 직접 실습하였습니다.

실제 서버 환경에서는 잘못된 Permission 설정이 보안 문제를 일으킬 수 있으므로 적절한 권한 설정이 중요하다는 점도 함께 학습하였습니다.

---

# 7. Docker 설치 및 실행 확인

Docker Desktop이 정상적으로 설치되었는지 확인하기 위해 Docker CLI 명령을 실행하였습니다.

---

## 7-1 Docker Version 확인

### 실행 명령

```bash
docker --version
```

### 실제 터미널 출력

```text
$ docker --version
Docker version 29.6.2, build dfc4efb
```

현재 Docker CLI가 정상적으로 설치되어 있으며 사용할 수 있는 상태임을 확인하였습니다.

📷 Docker Version 화면

---

## 7-2 Docker Engine 확인

Docker Client뿐 아니라 Docker Engine(Server)도 정상적으로 동작하는지 확인하기 위해 docker info 명령을 실행하였습니다.

### 실행 명령

```bash
docker info
```

### 실제 터미널 출력(일부)

```text
Client:
 Version:    29.6.2
 Context:    desktop-linux

 Plugins:
  buildx
  compose
  desktop
  scout
  ...

Server:

 Containers: 0
 Running: 0
 Stopped: 0

 Images: 1

 Storage Driver: overlayfs

 Cgroup Version: 2

 Operating System: Docker Desktop

 OSType: linux

 Architecture: x86_64

 CPUs: 8

 Total Memory: 7.527GiB

 Docker Root Dir: /var/lib/docker
```

📷 docker info 실행 화면

---

### 결과 분석

docker info 명령을 통해

- Docker Client
- Docker Server
- 현재 실행 중인 Container
- 저장된 Image
- CPU
- 메모리
- Storage Driver
- Docker Root Directory

등 다양한 정보를 확인할 수 있었습니다.

특히

```
OSType : linux
```

와

```
Kernel Version

6.18.x-microsoft-standard-WSL2
```

를 통해 Windows 환경이지만 WSL2 기반 Linux Kernel 위에서 Docker가 실행되고 있음을 확인할 수 있었습니다.

---

### Docker Client와 Docker Daemon

이번 실습을 통해 Docker는 크게 두 부분으로 구성된다는 것을 알게 되었습니다.

```
Docker CLI

↓

Docker Daemon

↓

Container 생성
```

사용자가 입력하는

```bash
docker run
docker build
docker ps
```

같은 명령은 Docker Client가 받아 Docker Daemon에게 전달합니다.

실제로 이미지를 생성하거나 컨테이너를 실행하는 작업은 Docker Daemon이 수행합니다.

이번 docker info 명령을 통해 Client와 Server가 정상적으로 통신하고 있음을 확인할 수 있었습니다.

---

# 8. Hello World 실행

Docker 설치가 정상적으로 완료되었는지 확인하기 위해 공식 hello-world 이미지를 실행하였습니다.

Hello World 이미지는 Docker 설치 여부를 가장 간단하게 확인할 수 있는 테스트 이미지입니다.

---

## 8-1 hello-world 실행

### 실행 명령

```bash
docker run hello-world
```

### 실제 터미널 출력

```text
$ docker run hello-world

Unable to find image 'hello-world:latest' locally

latest: Pulling from library/hello-world

4f55086f7dd0: Pull complete

d5e71e642bf5: Download complete

Digest: sha256:7f4da0fc94bcece205a8c0b6f4d11c8196924654ffe5c4d1aa439b7f632048b2

Status: Downloaded newer image for hello-world:latest

Hello from Docker!

This message shows that your installation appears to be working correctly.

The Docker client contacted the Docker daemon.

The Docker daemon pulled the image from Docker Hub.

The Docker daemon created a new container.

The Docker daemon streamed that output to the Docker client.
```

📷 hello-world 실행 화면

---

### 실행 과정 분석

이번 명령을 실행했을 때 Docker는 아래 순서대로 동작하였습니다.

```
docker run hello-world

↓

Local Image 확인

↓

Image 없음

↓

Docker Hub 접속

↓

hello-world 다운로드

↓

Container 생성

↓

Container 실행

↓

실행 결과 출력

↓

Container 종료
```

처음 실행했기 때문에

```
Unable to find image locally
```

메시지가 출력되었습니다.

이는 오류가 아니라

로컬 PC에 hello-world 이미지가 존재하지 않는다는 의미입니다.

Docker는 자동으로 Docker Hub에서 이미지를 다운로드한 후 실행하였습니다.

---

## 이번 실습에서 배운 점

이번 실습을 통해 Docker는 이미지를 기반으로 컨테이너를 생성한다는 개념을 직접 확인할 수 있었습니다.

또한 로컬에 이미지가 없을 경우 Docker Hub에서 자동으로 이미지를 내려받아 실행한다는 점도 확인하였습니다.

Hello World는 단순한 출력 프로그램이지만 Docker Engine이 정상적으로 설치되어 있고 Client와 Daemon이 올바르게 통신하고 있는지 확인하는 가장 기본적인 테스트라는 것을 이해할 수 있었습니다.

---
# 13. Docker Compose 실습

이번 실습에서는 여러 개의 Docker 명령어를 하나씩 실행하는 대신, docker-compose.yml 파일을 이용하여 컨테이너를 한 번에 관리하는 방법을 실습하였다.

Docker Compose를 사용하면 이미지 빌드부터 컨테이너 생성 및 실행까지 하나의 명령어만으로 처리할 수 있어 프로젝트 관리가 훨씬 편리하다.

---

## 13-1 docker-compose.yml 작성

이번 프로젝트에서 작성한 docker-compose.yml은 다음과 같다.

```yaml
services:
  my-web:
    build: .
    container_name: my-web-container
    ports:
      - "8080:80"
```

### 코드 설명

#### build

```yaml
build: .
```

현재 디렉터리에 존재하는 Dockerfile을 이용하여 이미지를 생성한다.

즉,

```
docker build
```

명령을 별도로 실행하지 않아도 Compose가 자동으로 Build를 수행한다.

---

#### container_name

```yaml
container_name: my-web-container
```

실행되는 컨테이너 이름을 지정한다.

랜덤한 이름 대신 원하는 이름으로 관리할 수 있어 여러 컨테이너를 사용할 때 식별하기 쉽다.

---

#### ports

```yaml
ports:
  - "8080:80"
```

Host의 8080 포트와 Container의 80 포트를 연결한다.

브라우저에서는

```
http://localhost:8080
```

으로 접속하면 컨테이너 내부 nginx 웹 서버에 접근할 수 있다.

---

## 13-2 Docker Compose 실행

실행 명령

```bash
docker-compose up -d
```

실행 결과

```text
time="2026-08-05T21:35:21+09:00" level=warning msg="docker-compose.yml: the attribute `version` is obsolete"

#1 [internal] load local bake definitions

#2 [internal] load build definition from Dockerfile

#3 [internal] load metadata for docker.io/library/nginx:latest

#4 [auth] library/nginx:pull token

#5 [internal] load .dockerignore

#6 [internal] load build context

#7 [1/2] FROM docker.io/library/nginx:latest

#8 [2/2] COPY index.html /usr/share/nginx/html/index.html

#9 exporting to image

#9 naming to docker.io/library/practice-my-web:latest

#10 resolving provenance

[+] Running 3/3

✔ Image practice-my-web Built

✔ Network practice_default Created

✔ Container my-web-container Started
```

---

### 실행 과정 분석

Docker Compose는 다음 순서로 자동 수행된다.

1. Dockerfile 확인
2. nginx 이미지 확인
3. 필요한 경우 Docker Hub에서 다운로드
4. Docker Image Build
5. Network 생성
6. Container 생성
7. Container 실행

즉,

기존에는

```
docker build

↓

docker run
```

을 각각 실행했지만,

Compose에서는

```
docker-compose up -d
```

명령 하나만으로 모두 수행된다.

---

## Warning 메시지 확인

실행 중 아래와 같은 Warning이 발생하였다.

```text
the attribute version is obsolete
```

이는 docker-compose.yml에 작성했던

```yaml
version: "3"
```

항목이 최신 Docker Compose에서는 더 이상 사용되지 않기 때문에 출력되는 경고이다.

프로젝트 실행에는 문제가 없었으며,

version 항목을 삭제하면 Warning도 사라진다.

이번 실습에서는 Docker Compose 버전 변경에 따른 차이도 함께 확인할 수 있었다.

📷 Docker Compose 실행 화면 첨부

---

# 이번 실습에서 배운 점

- docker-compose.yml 하나로 프로젝트를 관리할 수 있다.
- docker build와 docker run을 따로 실행하지 않아도 된다.
- 여러 컨테이너 프로젝트에서 더욱 효율적으로 사용할 수 있다.
- Docker Compose는 자동으로 Network도 생성한다.
- 최신 Compose에서는 version 속성이 더 이상 필요하지 않다.

### 14. Git & GitHub

이번 프로젝트에서는 실습 내용을 Git으로 관리하고 GitHub 원격 저장소에 업로드하였다.

Git을 이용하여 변경사항을 기록하고 프로젝트 진행 과정을 관리하였다.

## 14-1 Git Staging
모든 변경사항을 Staging Area에 추가하였다.

 ```bash
git add .
 ```
 현재 변경된 모든 파일을 Commit 대상으로 등록한다.

 ## 14-2 Commit
 실행 명령
 ```bash
 git commit -m "Add docker-compose and update README"
 ```
 실행 결과
 ```text
 [main bf5dd37]

Add docker-compose and update README

4 files changed

38 insertions(+)

create mode 100644 practice/Dockerfile

create mode 100644 practice/docker-compose.yml

create mode 100644 practice/index.html

create mode 100644 practice/test.txt
```

Commit 메시지를 이렇게 작성한 이유

Commit은 단순히 저장하는 것이 아니라

"무엇을 변경했는지"

기록하는 기능이다.

이번 Commit에서는

Docker Compose 추가
README 수정

두 가지 작업을 수행했기 때문에 이를 Commit 메시지에 명확하게 작성하였다.

📷 Commit 화면 첨부

## 14-3 GitHub Push
실행 명령
```bash
git push origin main
```
실행 결과
```text
Enumerating objects: 8, done.

Counting objects: 100% (8/8), done.

Compressing objects: 100% (6/6), done.

Writing objects: 100% (7/7)

To https://github.com/gunhee0402/codyssey-1.git

b73900b..bf5dd37

main -> main
```
Push를 통해 로컬 저장소의 변경사항을 GitHub 원격 저장소에 업로드하였다.

### 루트 디렉터리 README 수정
practice 폴더 작업이 끝난 뒤,
상위 프로젝트 README도 수정하였다.

실행 명령
```bash
cd ..

git add .

git commit -m "Update README and project files"

git push origin main
```

실행 결과
```text
[main 428d572]

Update README and project files

1 file changed

18 insertions(+)

10 deletions(-)

To https://github.com/gunhee0402/codyssey-1.git

bf5dd37..428d572

main -> main
```

이번 프로젝트에서는 실습 내용뿐 아니라 README도 지속적으로 수정하며 프로젝트 진행 과정을 기록하였다.

📷 GitHub Push 화면 첨부

### Git을 사용하면서 느낀 점
이번 실습을 통해 Git은 단순한 백업 도구가 아니라 프로젝트의 변경 이력을 관리하는 도구라는 점을 알 수 있었다.

특히 README를 수정한 후 Commit을 여러 번 수행하면서 기능 단위로 기록을 남기는 것이 이후 프로젝트를 관리할 때 큰 도움이 된다는 것을 경험하였다.

GitHub에 Push한 뒤에는 언제든지 다른 컴퓨터에서도 Clone하여 동일한 프로젝트를 이어서 작업할 수 있다는 점도 확인하였다.

# 15. 실습 중 발생한 오류 및 해결 과정

이번 프로젝트에서는 Linux CLI, Docker, Docker Compose를 처음 사용하면서 여러 가지 오류를 경험하였다.

오류가 발생한 원인을 확인하고 해결하는 과정을 통해 단순히 명령어를 실행하는 것보다 문제를 분석하는 과정이 중요하다는 것을 느낄 수 있었다.

---

## 오류 1. Dockerfile이 비어있는 상태에서 Build 수행

### 실행 명령

```bash
docker build -t my-web-server .
```

실행 결과

```text
ERROR: failed to build:

failed to solve:

the Dockerfile cannot be empty
```

### 원인

Docker Build는 현재 디렉터리의 Dockerfile을 읽어 이미지를 생성한다.

하지만 처음에는 Dockerfile이 비어 있었기 때문에 어떤 이미지를 사용할지, 어떤 작업을 수행해야 하는지 알 수 없어 Build가 실패하였다.

### 해결

Dockerfile을 아래와 같이 작성한 후 다시 Build를 수행하였다.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

이후 Build가 정상적으로 완료되었다.

---

## 오류 2. 터미널 붙여넣기 오류

실행 결과

```text
$ [200~docker stop volume-test~

bash:

[200~docker:

command not found
```

### 원인

Git Bash에 명령어를 붙여넣는 과정에서 제어문자가 함께 입력되었다.

실제로 실행된 명령은

```
[200~docker stop volume-test
```

가 되어 Bash가 새로운 명령으로 인식하였다.

### 해결

명령어를 다시 입력하였다.

```bash
docker stop volume-test
docker rm volume-test
```

정상적으로 종료 및 삭제가 완료되었다.

---

## 오류 3. Docker Compose Warning

실행 결과

```text
the attribute version is obsolete
```

### 원인

docker-compose.yml에 작성되어 있던

```yaml
version: "3"
```

항목이 최신 Docker Compose에서는 더 이상 사용되지 않는다.

### 해결

프로젝트 실행에는 문제가 없었으며,

최신 Compose에서는 version 없이도 정상적으로 동작한다는 것을 확인하였다.

---

## 오류 4. 첫 번째 Hello World 실행

처음에는 hello-world 이미지가 존재하지 않아 아래와 같은 메시지가 출력되었다.

```text
Unable to find image 'hello-world:latest' locally
```

### 원인

PC 내부에 hello-world 이미지가 존재하지 않았기 때문이다.

### 해결

Docker Hub에서 자동으로 다운로드되었으며 이후에는 로컬 이미지를 사용하여 바로 실행되었다.

---

## 오류를 통해 배운 점

이번 프로젝트에서는 단순히 오류를 해결하는 것이 아니라,

오류 메시지를 읽고 원인을 분석하는 과정이 중요하다는 것을 알게 되었다.

특히 Docker는 오류 메시지가 비교적 자세하게 출력되므로 원인을 파악하는 데 많은 도움이 되었다.


# 16. 프로젝트 회고

이번 프로젝트는 Linux CLI와 Docker를 처음부터 직접 실습해 보면서 개발 환경이 어떻게 구성되는지 경험할 수 있었던 프로젝트였다.

평소에는 IDE에서만 개발을 진행했지만, 이번에는 터미널을 이용하여 파일을 생성하고 권한을 변경하며 Linux 명령어의 기본적인 사용 방법을 익힐 수 있었다.

Docker를 사용하면서는 Image와 Container의 차이를 이해할 수 있었고,

Dockerfile을 이용하여 직접 이미지를 생성하고,

Port Mapping과 Bind Mount를 활용하여 Host와 Container가 어떻게 연결되는지도 확인할 수 있었다.

특히 하나의 이미지를 이용하여 여러 개의 컨테이너를 실행할 수 있다는 점과,

Volume을 사용하면 컨테이너를 다시 생성하지 않아도 변경사항이 즉시 반영된다는 점이 가장 인상 깊었다.

또한 Docker Compose를 이용하면서 여러 Docker 명령어를 하나씩 입력하는 대신,

하나의 설정 파일만으로 프로젝트를 관리할 수 있다는 점도 경험할 수 있었다.

Git과 GitHub를 이용하여 기능을 추가할 때마다 Commit을 남기고,

원격 저장소에 Push하면서 프로젝트 변경 이력을 관리하는 방법도 익힐 수 있었다.

실습 과정에서는 Dockerfile 작성 오류, 터미널 입력 오류, Docker Compose Warning 등 다양한 문제도 발생했지만,

오류 메시지를 확인하고 원인을 찾아 해결하는 과정 자체가 좋은 경험이 되었다.

이번 프로젝트를 통해 Linux CLI, Docker, Docker Compose, Git을 실제로 사용해 볼 수 있었으며,

앞으로 진행하게 될 백엔드 개발이나 DevOps 환경에서도 이번 경험이 큰 도움이 될 것이라고 생각한다.

# 17. 사용한 주요 명령어

## Linux

```bash
pwd
mkdir
cd
touch
ls
ls -la
ls -l
chmod
```

## Docker

```bash
docker --version
docker info
docker run
docker build
docker ps
docker stop
docker rm
```

## Docker Compose

```bash
docker-compose up -d
```

## Git

```bash
git add .
git commit -m ""
git push origin main
git status
```

---

이번 프로젝트에서는 위 명령어들을 직접 실행하면서 각각의 역할과 사용 방법을 익힐 수 있었다.