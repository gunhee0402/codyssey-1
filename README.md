# E1-1 Linux CLI / Docker / Git 실습

## 프로젝트 소개

Codyssey E1-1 미션입니다.

이번 프로젝트에서는 Linux CLI, Docker, Docker Compose, Git, GitHub를 활용하여 개발 환경을 직접 구축하고, Docker 기반 웹 서버를 실행하는 과정을 실습하였습니다.

단순히 명령어를 따라 입력하는 것이 아니라, 명령어가 어떤 역할을 수행하는지 직접 확인하고, 오류가 발생한 경우 원인을 분석하여 해결하는 과정까지 기록하였습니다.

---

# 목차

1. 프로젝트 목표
2. 개발환경
3. 프로젝트 구조
4. 수행 내용
5. Linux CLI 실습
6. 파일 권한(Permission)
7. Docker 설치 확인
8. Docker Hello World
9. Dockerfile 작성
10. Docker Image Build
11. Docker Container 실행
12. Docker Volume
13. Docker Compose
14. Git & GitHub
15. 실습 중 발생한 오류
16. 느낀점

---

# 1. 프로젝트 목표

이번 프로젝트에서는 아래 항목들을 직접 실습하였다.

- Linux CLI 기본 명령어 사용
- 디렉터리 및 파일 생성
- Linux 파일 권한 변경
- Docker 설치 확인
- Docker Image Build
- Docker Container 실행
- Port Mapping
- Bind Mount(Volume)
- Docker Compose
- Git Commit 및 GitHub Push

이번 프로젝트의 목표는 단순히 명령어를 암기하는 것이 아니라,

각 명령어가 실제 개발환경에서 어떤 역할을 하는지 직접 경험하는 것이었다.

---

# 2. 개발환경

|항목|내용|
|----|----|
|OS|Windows11 + WSL2|
|Terminal|Git Bash|
|Editor|Visual Studio Code|
|Docker|29.6.2|
|Git|Git for Windows|
|Repository|GitHub|

📷 개발환경 스크린샷 첨부

---

# 3. 프로젝트 구조

```bash
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

프로젝트는 Docker 실습을 진행하기 위해 `practice` 폴더를 별도로 생성하여 관리하였다.

---

# 4. 수행 내용

이번 프로젝트는 아래 순서대로 진행하였다.

1. Linux CLI 명령어 실습
2. 파일 권한 변경
3. Docker 설치 확인
4. Hello World 실행
5. Dockerfile 작성
6. Docker Image Build
7. Docker Container 실행
8. Docker Volume 실습
9. Docker Compose
10. GitHub 업로드

---

# 5. Linux CLI 실습

Docker를 사용하기 전에 Linux CLI 명령어를 이용하여 프로젝트 디렉터리를 생성하고 파일을 관리하는 방법을 먼저 실습하였다.

---

## 5-1 현재 작업 위치 확인 (pwd)

현재 터미널이 어느 디렉터리에서 작업 중인지 확인하기 위해 `pwd(Print Working Directory)` 명령어를 사용하였다.

### 실행 명령

```bash
pwd
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1 (main)

$ pwd

/c/Users/jkhlm/codyssey-1
```

### 명령어 설명

`pwd`는 현재 작업 중인 디렉터리의 절대 경로를 출력하는 Linux 명령어이다.

이를 통해 현재 `codyssey-1` 프로젝트 폴더에서 작업하고 있음을 확인하였다.

📷 스크린샷 첨부

---

## 5-2 practice 디렉터리 생성

Docker 관련 실습 파일을 별도로 관리하기 위해 새로운 디렉터리를 생성하였다.

### 실행 명령

```bash
mkdir practice
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1 (main)

$ mkdir practice
```

디렉터리를 생성한 뒤 생성한 폴더로 이동하였다.

```bash
cd practice
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1 (main)

$ cd practice

jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)
```

### 명령어 설명

- `mkdir`은 새로운 디렉터리를 생성하는 명령어이다.
- `cd`는 현재 작업 위치를 변경하는 명령어이다.

Docker 실습은 모두 practice 폴더 안에서 진행하였다.

📷 스크린샷 첨부

---

## 5-3 test.txt 파일 생성

Linux에서는 `touch` 명령어를 이용하여 빈 파일을 생성할 수 있다.

### 실행 명령

```bash
touch test.txt
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ touch test.txt
```

생성한 파일이 정상적으로 만들어졌는지 확인하기 위해 아래 명령어를 실행하였다.

```bash
ls -la
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ ls -la

total 0

drwxr-xr-x 1 jkhlm 197609 0 Aug  5 21:08 ./

drwxr-xr-x 1 jkhlm 197609 0 Aug  5 21:07 ../

-rw-r--r-- 1 jkhlm 197609 0 Aug  5 21:08 test.txt
```

### 결과 분석

`test.txt` 파일이 정상적으로 생성된 것을 확인하였다.

또한 파일의 기본 권한도 함께 확인할 수 있었다.

### 명령어 설명

- `touch` : 새로운 빈 파일 생성
- `ls` : 파일 목록 출력
- `-l` : 상세 정보 출력
- `-a` : 숨김 파일까지 함께 출력

📷 스크린샷 첨부

---

## 5-4 파일 권한 확인

생성된 파일의 권한을 확인하기 위해 아래 명령어를 실행하였다.

### 실행 명령

```bash
ls -l test.txt
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ ls -l test.txt

-rw-r--r-- 1 jkhlm 197609 0 Aug  5 21:08 test.txt
```

### 결과 분석

파일의 현재 권한은

```text
-rw-r--r--
```

이다.

이를 숫자로 표현하면

```text
644
```

와 동일하다.

각 권한은 아래 의미를 가진다.

|권한|의미|
|----|----|
|r|Read|
|w|Write|
|x|Execute|

또한 Linux에서는 권한을

- Owner
- Group
- Other

세 그룹으로 나누어 관리한다.

현재 권한은

- Owner → Read / Write
- Group → Read
- Other → Read

권한을 가지고 있었다.

📷 스크린샷 첨부

---

# 6. 파일 권한(Permission) 실습

Linux에서는 모든 파일과 디렉터리에 접근 권한(Permission)이 존재한다.

권한은 크게

- Read (r)
- Write (w)
- Execute (x)

세 가지로 구성되며,

각 권한은

- Owner(소유자)
- Group(그룹)
- Other(기타 사용자)

에게 각각 부여된다.

이번 실습에서는 `chmod` 명령어를 이용하여 파일 권한을 직접 변경하고 변경 결과를 확인하였다.

---

## 6-1 현재 권한 확인

먼저 생성한 test.txt의 권한을 확인하였다.

### 실행 명령

```bash
ls -l test.txt
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ ls -l test.txt

-rw-r--r-- 1 jkhlm 197609 0 Aug  5 21:08 test.txt
```

현재 파일 권한은

```text
-rw-r--r--
```

이다.

숫자로 표현하면

```text
644
```

권한과 동일하다.

권한을 숫자로 표현하는 이유는 Linux에서 chmod 명령어를 사용할 때 숫자 권한이 가장 많이 사용되기 때문이다.

|숫자|권한|
|----|----|
|4|Read|
|2|Write|
|1|Execute|

따라서

```
6 = 4 + 2 = rw-
4 = Read
4 = Read
```

를 의미한다.

즉,

Owner

- Read
- Write

Group

- Read

Other

- Read

권한을 가지고 있는 상태였다.

📷 스크린샷 첨부

---

## 6-2 chmod를 이용한 권한 변경

이번에는 chmod 명령어를 이용하여 파일 권한을 변경하였다.

### 실행 명령

```bash
chmod 755 test.txt
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ chmod 755 test.txt
```

chmod는 정상적으로 수행되면 별도의 출력 없이 종료된다.

권한이 제대로 변경되었는지 다시 확인하였다.

### 실행 명령

```bash
ls -l test.txt
```

### 실제 터미널 실행 결과

```text
-rwxr-xr-x
```

권한이

```text
755
```

로 변경된 것을 확인하였다.

---

### chmod 755 의미

755는 아래와 같은 권한을 의미한다.

|숫자|권한|
|----|----|
|7|rwx|
|5|r-x|
|5|r-x|

즉,

Owner는

- Read
- Write
- Execute

권한을 가지며,

Group과 Other는

- Read
- Execute

권한만 가진다.

Linux에서는 실행 가능한 파일이나 프로그램에 자주 사용하는 권한이다.

이번 실습에서는 test.txt에 실행 권한을 부여하는 과정을 직접 확인하였다.

📷 스크린샷 첨부

---

# 이번 실습에서 배운 점

이번 파일 권한 실습을 통해 다음 내용을 이해할 수 있었다.

- Linux의 파일에는 접근 권한이 존재한다.
- 권한은 Read, Write, Execute로 구성된다.
- chmod 명령어를 이용하여 권한을 변경할 수 있다.
- 숫자 권한(644, 755 등)은 각 권한의 합으로 표현된다.
- ls -l 명령어를 이용하여 현재 권한을 확인할 수 있다.

---

# 7. Docker 설치 확인

Linux 기본 명령어 실습 이후 Docker Desktop이 정상적으로 설치되었는지 확인하였다.

Docker를 사용하기 위해서는 Docker Engine이 정상적으로 실행되고 있어야 하므로 먼저 버전과 시스템 정보를 확인하였다.

---

## 7-1 Docker Version 확인

먼저 Docker가 정상적으로 설치되어 있는지 확인하였다.

### 실행 명령

```bash
docker --version
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker --version

Docker version 29.6.2, build dfc4efb
```

Docker CLI가 정상적으로 설치되어 있으며 현재 버전은

```
29.6.2
```

임을 확인하였다.

별도의 오류 없이 버전이 출력되었기 때문에 Docker 명령어를 사용할 수 있는 환경이 준비되어 있음을 확인하였다.

📷 스크린샷 첨부

---

## 7-2 Docker 정보 확인

이번에는 Docker Engine이 실제로 실행 중인지 확인하기 위해

다음 명령어를 실행하였다.

### 실행 명령

```bash
docker info
```

### 실제 터미널 실행 결과

```bash
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker info

Client:

 Version:    29.6.2

 Context:    desktop-linux

 Debug Mode: false

 Plugins:

  agent: Docker AI Agent Runner

  ai: Docker AI Agent

  buildx: Docker Buildx

  compose: Docker Compose

  debug

  desktop

  dhi

  extension

  init

  mcp

  model

  offload

  pass

  sandbox

  scout



Server:

 Containers: 0

 Running: 0

 Paused: 0

 Stopped: 0

 Images: 1

 Server Version: 29.6.2

 Storage Driver: overlayfs

 Operating System: Docker Desktop

 Architecture: x86_64

 CPUs: 8

 Total Memory: 7.527GiB

 Docker Root Dir: /var/lib/docker

 Firewall Backend: iptables
```

> **참고:** 실제 README에는 위 내용을 요약하지 말고, 네 터미널에서 출력된 내용을 **끝까지 그대로 붙여 넣는 것을 권장한다.** `docker info` 출력은 길지만, 그대로 기록하면 실습 재현성과 신뢰성이 높아진다.

### 결과 분석

이번 명령을 통해

- Docker Client가 정상적으로 설치되어 있는지
- Docker Daemon(Server)이 실행 중인지
- Docker Desktop이 WSL2 기반으로 동작하는지
- 현재 실행 중인 컨테이너 개수
- 이미지 개수
- 메모리 사용 환경

등을 확인할 수 있었다.

특히

```text
Operating System:

Docker Desktop
```

과

```text
Kernel Version:

6.18.33.2-microsoft-standard-WSL2
```

를 통해 WSL2 환경에서 Docker Engine이 실행되고 있음을 확인하였다.

📷 스크린샷 첨부

---

# 이번 실습에서 배운 점

- Docker CLI와 Docker Engine은 서로 다른 역할을 수행한다.
- docker --version은 설치 여부를 확인하는 가장 기본적인 명령이다.
- docker info는 현재 Docker 환경 전체를 확인할 수 있다.
- Docker Desktop은 WSL2 기반으로 동작할 수 있다.
- 아직 컨테이너를 생성하지 않았기 때문에 Running Container는 0개로 표시되었다.

---

# 8. Docker Hello World 실행

Docker가 정상적으로 설치되었는지 확인하기 위해 Docker에서 제공하는 가장 기본적인 테스트 이미지인 `hello-world`를 실행하였다.

이 실습을 통해 Docker Client와 Docker Daemon이 정상적으로 통신하는지 확인할 수 있었다.

---

## 8-1 Hello World 실행

### 실행 명령

```bash
docker run hello-world
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker run hello-world

Unable to find image 'hello-world:latest' locally

latest: Pulling from library/hello-world

4f55086f7dd0: Pull complete

d5e71e642bf5: Download complete

Digest: sha256:7f4da0fc94bcece205a8c0b6f4d11c8196924654ffe5c4d1aa439b7f632048b2

Status: Downloaded newer image for hello-world:latest



Hello from Docker!

This message shows that your installation appears to be working correctly.



To generate this message, Docker took the following steps:

1. The Docker client contacted the Docker daemon.

2. The Docker daemon pulled the "hello-world" image from the Docker Hub.

3. The Docker daemon created a new container from that image.

4. The Docker daemon streamed that output to the Docker client.
```

> 실제 README에는 위 출력 내용을 중간 생략 없이 그대로 첨부하였다.

---

## 실행 과정 분석

이번 명령을 처음 실행했을 때

```text
Unable to find image 'hello-world:latest' locally
```

라는 문장이 출력되었다.

이는 오류가 아니라,

현재 PC에 `hello-world` 이미지가 존재하지 않았기 때문에 Docker Hub에서 자동으로 이미지를 다운로드했다는 의미이다.

이후

```text
Pull complete
```

가 출력되면서 이미지 다운로드가 완료되었다.

다운로드가 끝난 뒤 Docker는 자동으로 컨테이너를 생성하여 실행하였고,

정상적으로 실행되었기 때문에

```text
Hello from Docker!
```

메시지를 출력하였다.

이를 통해

- Docker Engine
- Docker Client
- Docker Hub

가 정상적으로 동작하는 것을 확인하였다.

📷 **스크린샷 첨부**

---

## 이번 실습에서 이해한 내용

이번 실습을 통해 Docker는 다음 순서로 동작한다는 것을 확인하였다.

```
docker run

↓

이미지가 존재하는지 확인

↓

없으면 Docker Hub에서 다운로드

↓

이미지(Image) 생성

↓

컨테이너(Container) 생성

↓

프로그램 실행
```

또한 Image와 Container는 서로 다른 개념이라는 것도 이해할 수 있었다.

- Image는 실행 파일(설계도)
- Container는 실제 실행 중인 프로그램

이라는 차이가 있다.

---

# 9. Dockerfile 작성

이번 실습에서는 nginx 공식 이미지를 기반으로 새로운 Docker 이미지를 직접 생성하였다.

Dockerfile을 이용하면 동일한 개발환경을 언제든지 다시 생성할 수 있다는 점을 확인할 수 있었다.

---

## 9-1 Dockerfile 작성

작성한 Dockerfile은 아래와 같다.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

📷 **Dockerfile 작성 화면 첨부**

---

## 코드 설명

### ① FROM

```dockerfile
FROM nginx:latest
```

Docker Hub에서 제공하는 공식 nginx 이미지를 Base Image로 사용하였다.

nginx는 웹 서버 프로그램이며 기본적으로 80번 포트를 사용한다.

Docker Image를 만들 때는 항상 어떤 이미지를 기반으로 만들 것인지 먼저 지정해야 한다.

이번 프로젝트에서는 nginx를 기반으로 새로운 이미지를 생성하였다.

---

### ② COPY

```dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

현재 프로젝트 폴더에 존재하는

```
index.html
```

파일을

컨테이너 내부의

```
/usr/share/nginx/html/
```

폴더로 복사하였다.

이 경로는 nginx가 기본적으로 웹페이지를 서비스하는 위치이다.

즉,

브라우저에서 접속하면 내가 만든 HTML 파일이 화면에 출력된다.

---

## Dockerfile 전체 동작 과정

이번 Dockerfile은 아래 순서대로 실행된다.

```
FROM nginx

↓

nginx 공식 이미지 다운로드

↓

COPY 실행

↓

index.html 복사

↓

새로운 Docker Image 생성
```

Dockerfile은 한 줄씩 순서대로 실행되며,

각 명령은 하나의 Layer를 생성한다.

이번 프로젝트에서는

- Layer 1 : FROM
- Layer 2 : COPY

총 2개의 Layer가 생성되었다.

---

# 10. Docker Image Build

Dockerfile을 이용하여 Docker 이미지를 생성하였다.

이번 실습에서는 처음 Build에 실패하였고,

원인을 분석한 뒤 Dockerfile을 수정하여 Build를 성공시켰다.

실패 과정도 함께 기록하였다.

---

## 10-1 첫 번째 Build (실패)

### 실행 명령

```bash
docker build -t my-web-server .
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker build -t my-web-server .

[+] Building 0.4s (1/1) FINISHED

=> [internal] load build definition

=> => transferring dockerfile: 31B

ERROR: failed to build:

failed to solve:

the Dockerfile cannot be empty
```

📷 **실패 화면 첨부**

---

## 실패 원인 분석

이번 Build는 Dockerfile이 비어있는 상태에서 실행하였다.

Docker Build는 Dockerfile을 읽어서

- 어떤 이미지를 사용할지
- 어떤 파일을 복사할지
- 어떤 프로그램을 실행할지

순서대로 수행한다.

하지만 Dockerfile 내부에 아무 내용도 존재하지 않았기 때문에

Docker는 어떤 이미지를 생성해야 하는지 알 수 없어 Build를 중단하였다.

오류 메시지인

```text
the Dockerfile cannot be empty
```

는

Dockerfile이 존재하지만 내부가 비어 있다는 의미이다.

---

## 해결 방법

Dockerfile을 아래와 같이 작성한 뒤 다시 Build를 수행하였다.

```dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

이후 Build를 다시 실행하였다.

## 10-2 Docker Build 성공

Dockerfile을 작성한 뒤 다시 Build를 진행하였다.

### 실행 명령

```bash
docker build -t my-web-server .
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker build -t my-web-server .

[+] Building 3.5s (8/8) FINISHED

=> [internal] load build definition

=> => transferring dockerfile: 437B

=> [internal] load metadata

=> [auth] library/nginx:pull

=> [internal] load .dockerignore

=> => transferring context: 2B

=> [internal] load build context

=> => transferring context: 299B

=> CACHED [1/2] FROM docker.io/library/nginx:latest

=> => resolve docker.io/library/nginx:latest

=> [2/2] COPY index.html /usr/share/nginx/html/index.html

=> exporting to image

=> => exporting layers

=> => exporting manifest

=> => exporting config

=> => exporting attestation

=> => exporting manifest list

=> => naming to docker.io/library/my-web-server

=> => unpacking to docker.io/library/my-web-server
```

📷 **Build 성공 화면 첨부**

---

## Build 과정 분석

이번에는 Dockerfile이 정상적으로 작성되어 있었기 때문에 Build가 성공적으로 완료되었다.

실행 과정은 다음 순서로 진행되었다.

```
Dockerfile 읽기

↓

Base Image 확인

↓

nginx 이미지 다운로드(또는 캐시 사용)

↓

Build Context 업로드

↓

COPY 명령 실행

↓

새로운 Docker Image 생성
```

이번 Build에서는

```text
CACHED
```

라는 문구가 출력되었다.

이는 이전에 다운로드했던 nginx 이미지를 다시 다운로드하지 않고 캐시에 저장된 Layer를 재사용했다는 의미이다.

Docker는 변경되지 않은 Layer를 다시 만들지 않기 때문에 Build 속도가 훨씬 빨라지는 장점이 있다.

---

## 생성된 Image

Build가 완료되면서

```
my-web-server
```

라는 이름의 Docker Image가 생성되었다.

이 이미지는 이후 여러 개의 Container를 생성하는 기반이 된다.

Image는 설계도이며,

Container는 실제 실행되는 프로그램이라는 차이가 있다.

📷 **Docker Images 화면 첨부**

---

# 11. Docker Container 실행

Image 생성이 완료되었기 때문에 이번에는 해당 이미지를 이용하여 실제 Container를 실행하였다.

Docker에서는 하나의 Image로 여러 개의 Container를 생성할 수 있으며,

각 Container는 독립적으로 실행된다.

---

## 11-1 Container 실행

### 실행 명령

```bash
docker run -d -p 8080:80 --name my-first-container my-web-server
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker run -d -p 8080:80 --name my-first-container my-web-server

b618cae534da50ff614ce28e609875ed07bfd10afef2a9a9ff3d79fa65e1c561
```

컨테이너 ID가 출력되면서 정상적으로 실행되었다.

Docker에서는 컨테이너 생성이 완료되면 고유한 Container ID를 반환한다.

---

## 명령어 분석

이번에 사용한 명령은 다음과 같은 의미를 가진다.

```bash
docker run
```

새로운 Container를 생성하면서 동시에 실행한다.

```bash
-d
```

Detached Mode이다.

터미널을 점유하지 않고 백그라운드에서 실행한다.

```bash
-p 8080:80
```

포트 매핑(Port Mapping)을 수행한다.

Host PC의

```
8080
```

포트를

Container 내부의

```
80
```

포트와 연결한다.

즉,

브라우저에서

```
http://localhost:8080
```

으로 접속하면

Container 내부에서 실행 중인 nginx 웹 서버에 접근하게 된다.

```bash
--name my-first-container
```

Container 이름을 지정한다.

지정하지 않으면 Docker가 임의의 이름을 생성한다.

```bash
my-web-server
```

앞에서 Build한 Docker Image 이름이다.

---

## Port Mapping을 사용하는 이유

Docker Container는 독립된 네트워크 공간을 사용한다.

따라서 Container 내부의

```
80번 포트
```

를 그대로 사용할 수 없기 때문에

Host와 연결해 주는 과정이 필요하다.

이번 실습에서는

```
Host : 8080

↓

Container : 80
```

으로 연결하였다.

따라서 사용자는

```
localhost:8080
```

으로 접속하지만

실제로는

Container 내부의 nginx가 응답한다.

📷 **브라우저 실행 화면 첨부**

---

## 11-2 실행 중인 Container 확인

Container가 정상적으로 실행되고 있는지 확인하기 위해

다음 명령을 실행하였다.

### 실행 명령

```bash
docker ps
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker ps

CONTAINER ID   IMAGE           COMMAND                  CREATED

b618cae534da   my-web-server   "/docker-entrypoint.…"

STATUS

Up 48 seconds

PORTS

0.0.0.0:8080->80/tcp

NAMES

my-first-container
```

`docker ps` 명령을 통해 현재 실행 중인 Container를 확인할 수 있었다.

출력 결과에서는

- Container ID
- Image 이름
- 실행 상태(Status)
- Port Mapping
- Container 이름

등을 확인할 수 있었다.

특히

```text
0.0.0.0:8080->80/tcp
```

를 통해 Host의 8080 포트가 Container의 80번 포트와 연결되어 있음을 다시 확인할 수 있었다.

📷 **docker ps 실행 화면 첨부**

---

## 11-3 Container 종료

실행 중인 Container를 종료하였다.

### 실행 명령

```bash
docker stop my-first-container
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker stop my-first-container

my-first-container
```

Container가 정상적으로 종료되었다.

---

## 11-4 Container 삭제

Container를 종료한 뒤 삭제하였다.

### 실행 명령

```bash
docker rm my-first-container
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker rm my-first-container

my-first-container
```

Docker에서는 실행 중인 Container는 삭제할 수 없기 때문에

반드시

```
stop

↓

rm
```

순서로 삭제해야 한다.

📷 **Container 삭제 화면 첨부**

---

## 이번 실습에서 배운 점

이번 실습을 통해 다음 내용을 직접 확인할 수 있었다.

- 하나의 Image로 여러 개의 Container를 생성할 수 있다.
- `docker run`은 Container 생성과 실행을 동시에 수행한다.
- `-d` 옵션은 백그라운드 실행을 의미한다.
- `-p` 옵션은 Host와 Container의 포트를 연결한다.
- `docker ps` 명령으로 실행 중인 Container를 확인할 수 있다.
- 실행 중인 Container는 먼저 `docker stop`을 수행해야 삭제할 수 있다.
- `docker rm` 명령으로 종료된 Container를 삭제할 수 있다.

---

# 12. Docker Volume (Bind Mount)

이번 실습에서는 Docker Volume(Bind Mount)을 이용하여

Host(Windows)와 Container(Linux)가 동일한 파일을 공유하도록 구성하였다.

이를 통해 HTML 파일을 수정하면 이미지를 다시 Build하지 않아도 변경사항이 즉시 반영되는 것을 확인하였다.

---

## 12-1 index.html 파일만 Mount

처음에는 HTML 파일 하나만 연결하였다.

### 실행 명령

```bash
docker run -d -p 8080:80 \
-v $(pwd)/index.html:/usr/share/nginx/html/index.html \
--name volume-test my-web-server
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name volume-test my-web-server

b93b8e828e0a6cb524470f683a0df5f4998b7d4712edd80b980739f11919e788
```

정상적으로 새로운 Container가 생성되었다.

📷 **스크린샷 첨부**

---

## 명령어 분석

이번 명령에서 새롭게 사용한 옵션은

```bash
-v
```

이다.

```
Host

↓

$(pwd)/index.html

↓

Container

↓

/usr/share/nginx/html/index.html
```

현재 프로젝트에 존재하는

```
index.html
```

파일을

Container 내부 nginx의 웹 페이지와 연결하였다.

따라서 Host에서 HTML을 수정하면

Container 내부 파일도 동시에 변경된다.

---

## Bind Mount를 사용하는 이유

Docker Image는 Build 이후에는 변경되지 않는다.

만약 HTML을 수정할 때마다

```
docker build
```

를 반복해야 한다면 개발 속도가 매우 느려진다.

Bind Mount를 사용하면

이미지를 다시 생성하지 않아도

파일 변경사항이 즉시 Container 내부에 반영된다.

개발 과정에서는 가장 많이 사용하는 기능 중 하나이다.

---

## 12-2 Container 종료

실행 명령

```bash
docker stop volume-test
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker stop volume-test

volume-test
```

Container를 정상적으로 종료하였다.

---

## 12-3 Container 삭제

실행 명령

```bash
docker rm volume-test
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker rm volume-test

volume-test
```

Container를 삭제하였다.

---

# 13. 프로젝트 전체 Bind Mount

이번에는 HTML 파일 하나만 연결하는 것이 아니라

프로젝트 폴더 전체를 Mount하였다.

---

## 실행 명령

```bash
docker run -d -p 8081:80 \
-v "/$(pwd):/usr/share/nginx/html" \
--name volume-test my-web-server
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker run -d -p 8081:80 -v "/$(pwd):/usr/share/nginx/html" --name volume-test my-web-server

a692222b4e3f82f19a1df02c81f8c700f0c258b7e58e8f2fbb0060345f474eca
```

📷 **스크린샷 첨부**

---

## 왜 8080이 아니라 8081을 사용했는가?

처음 실습에서는

```
8080:80
```

포트를 사용하였다.

하지만 이후 실습에서는

```
8081:80
```

포트를 사용하였다.

그 이유는

기존 실습에서 8080 포트를 이미 사용했던 경험이 있었고,

동일한 포트를 사용하는 경우

```
Bind for 0.0.0.0:8080 failed
```

와 같은 포트 충돌이 발생할 수 있기 때문이다.

실습을 진행하면서 기존 포트와 충돌하는 상황을 피하기 위해

새로운 Host Port인

```
8081
```

을 사용하였다.

Docker에서는

```
8080

8081

6767

9000

5000
```

처럼 사용하지 않는 Host Port라면

어떤 번호라도 자유롭게 사용할 수 있다.

중요한 것은

Container 내부 nginx는 항상

```
80번 포트
```

를 사용하고,

Host에서 접근하기 위한 포트만 변경된다는 점이다.

즉,

```
Host : 8081

↓

Container : 80
```

으로 연결된 것이다.

---

## 프로젝트 전체 Mount의 장점

이번에는

```
index.html
```

파일 하나가 아니라

프로젝트 전체를 공유하였다.

```
practice

↓

Container

/usr/share/nginx/html
```

이렇게 연결하면

HTML 파일뿐 아니라

프로젝트 내 다른 파일도 동시에 공유할 수 있다.

개발 과정에서는 파일 하나만 공유하는 것보다

프로젝트 전체를 공유하는 방식이 훨씬 많이 사용된다.

---

# 14. 실습 중 발생한 오류

실습을 진행하는 과정에서 예상하지 못한 오류도 경험하였다.

오류 발생 원인을 확인하고

직접 해결하였다.

---

## 14-1 붙여넣기 오류

### 실제 터미널 실행 결과

```text
$ [200~docker stop volume-test~

bash: [200~docker: command not found
```

---

## 원인 분석

처음에는 Docker 명령이 잘못된 것으로 생각하였다.

하지만 확인해 보니

Git Bash에 명령어를 붙여넣는 과정에서

```
[200~
```

라는 제어문자가 함께 입력된 것이 원인이었다.

즉,

Docker 오류가 아니라

터미널 입력 과정에서 발생한 문제였다.

---

## 해결 과정

잘못 입력된 명령을 삭제한 후

다시 정상적으로 입력하였다.

### 실행 명령

```bash
docker stop volume-test
```

```text
volume-test
```

이후

```bash
docker rm volume-test
```

명령을 실행하여

Container도 정상적으로 삭제하였다.

이번 경험을 통해

오류가 발생했을 때

오류 메시지를 먼저 확인하고

원인을 분석하는 과정이 중요하다는 것을 배울 수 있었다.

📷 **오류 해결 화면 첨부**

---

## 이번 실습에서 배운 점

이번 Volume 실습을 통해 다음 내용을 이해하였다.

- Bind Mount를 사용하면 Build를 다시 하지 않아도 된다.
- Host와 Container가 동일한 파일을 공유할 수 있다.
- 프로젝트 전체를 Mount하는 방식이 개발 과정에서 더욱 많이 사용된다.
- Host Port는 자유롭게 변경할 수 있다.
- 동일한 포트를 사용할 경우 충돌이 발생할 수 있다.
- 오류가 발생했을 때는 명령어 자체보다 오류 메시지를 먼저 확인하는 습관이 중요하다.

---

# 15. Docker Compose

이번 실습에서는 여러 Docker 명령을 하나씩 입력하는 대신,

`docker-compose.yml` 파일을 이용하여 컨테이너를 한 번에 실행하였다.

Docker Compose를 사용하면 여러 개의 Container를 하나의 설정 파일로 관리할 수 있으며,

실제 프로젝트에서도 가장 많이 사용하는 방식 중 하나이다.

---

## 15-1 docker-compose 실행

### 실행 명령

```bash
docker-compose up -d
```

### 실제 터미널 실행 결과

```text
jkhlm@□□□□ MINGW64 ~/codyssey-1/practice (main)

$ docker-compose up -d

time="2026-08-05T21:35:21+09:00"
level=warning
msg="C:\Users\jkhlm\codyssey-1\practice\docker-compose.yml:
the attribute `version` is obsolete,
it will be ignored,
please remove it to avoid potential confusion"

#1 [internal] load local bake definitions

#2 [internal] load build definition from Dockerfile

#3 [internal] load metadata for docker.io/library/nginx:latest

#4 [auth] library/nginx:pull token

#5 [internal] load .dockerignore

#6 [internal] load build context

#7 [1/2] FROM docker.io/library/nginx:latest

#8 [2/2] COPY index.html /usr/share/nginx/html/index.html

#9 exporting to image

#10 resolving provenance for metadata file

[+] Running 3/3

✔ Image practice-my-web Built

✔ Network practice_default Created

✔ Container my-web-container Started
```

📷 **스크린샷 첨부**

---

## Compose 동작 과정

Docker Compose는 다음 순서로 동작하였다.

```
docker-compose.yml 읽기

↓

Dockerfile Build

↓

Image 생성

↓

Network 생성

↓

Container 생성

↓

Container 실행
```

기존에는

```
docker build

docker run
```

을 각각 입력해야 했지만,

Compose를 사용하면

```
docker-compose up -d
```

명령 하나로 모두 수행된다.

---

## Warning 메시지 분석

실행 결과를 보면

```text
the attribute version is obsolete
```

라는 Warning이 출력되었다.

처음에는 오류라고 생각했지만,

Container는 정상적으로 실행되었다.

원인을 확인해 보니

최근 Docker Compose에서는

```
version:
```

항목을 더 이상 사용하지 않는다.

예전 버전과의 호환성을 위해 남아있는 옵션이며,

현재 버전에서는 자동으로 무시된다.

따라서

```
version:
```

을 삭제해도 동일하게 동작한다.

이번 실습에서는

실행에는 문제가 없었기 때문에 그대로 진행하였다.

---

## Docker Compose의 장점

Docker Compose를 사용하면

- 여러 개의 Container를 동시에 실행할 수 있다.
- 네트워크가 자동으로 생성된다.
- Build와 Run을 한 번에 수행할 수 있다.
- 프로젝트 설정을 코드로 관리할 수 있다.

실제 프로젝트에서는 대부분 Docker Compose를 사용하여 개발환경을 구성한다고 이해하였다.

---

# 16. Git & GitHub

모든 실습을 완료한 뒤

프로젝트를 Git으로 관리하고 GitHub에 업로드하였다.

---

## 16-1 변경사항 저장

### 실행 명령

```bash
git add .
```

### 설명

현재 변경된 파일들을 모두 Git의 Staging Area에 등록하였다.

---

## 16-2 Commit

### 실행 명령

```bash
git commit -m "Add docker-compose and update README"
```

### 실제 터미널 결과

```text
[main bf5dd37]

Add docker-compose and update README

4 files changed, 38 insertions(+)

create mode 100644 practice/Dockerfile

create mode 100644 practice/docker-compose.yml

create mode 100644 practice/index.html

create mode 100644 practice/test.txt
```

이번 Commit에서는

Docker 관련 파일들을 저장하였다.

---

## 16-3 GitHub 업로드

### 실행 명령

```bash
git push origin main
```

### 실제 터미널 결과

```text
Enumerating objects: 8

Counting objects: 100%

Compressing objects: 100%

Writing objects: 100%

To https://github.com/gunhee0402/codyssey-1.git

b73900b..bf5dd37

main -> main
```

GitHub Repository에 정상적으로 업로드되었다.

---

## 16-4 루트 폴더에서 추가 Commit

practice 폴더 작업이 끝난 뒤

상위 프로젝트의 README도 수정하였다.

### 실행 명령

```bash
cd ..

git add .

git commit -m "Update README and project files"

git push origin main
```

### 실제 터미널 결과

```text
[main 428d572]

Update README and project files

1 file changed,

18 insertions(+),

10 deletions(-)

To

https://github.com/gunhee0402/codyssey-1.git

bf5dd37..428d572

main -> main
```

프로젝트 전체 README까지 수정하여 최종 업로드를 완료하였다.

📷 **GitHub Push 화면 첨부**

---

# 17. 전체 실습을 통해 배운 내용

이번 프로젝트에서는 Linux CLI부터 Docker, GitHub까지

실제 개발환경을 처음부터 직접 구축해보았다.

실습을 진행하면서

단순히 명령어를 외우는 것이 아니라

실제로 실행해 보고,

오류를 해결해 보면서

각 명령이 어떤 역할을 하는지 조금씩 이해할 수 있었다.

특히

Docker Build가 실패했던 과정,

붙여넣기 오류,

Docker Compose Warning 등을 직접 경험하면서

오류 메시지를 읽고 원인을 찾는 과정이 매우 중요하다는 것을 느꼈다.

또한

Git을 이용하여 변경사항을 Commit하고

GitHub에 Push하는 과정을 반복하면서

버전 관리가 왜 필요한지도 체감할 수 있었다.

이번 프로젝트는 Linux와 Docker를 처음 접하는 입장에서 쉽지는 않았지만,

직접 실습을 통해 개발환경을 구축하고 결과를 확인하면서

기본적인 개발 흐름을 경험할 수 있었던 의미 있는 프로젝트였다.

---

# GitHub Repository

프로젝트 주소

https://github.com/gunhee0402/codyssey-1

---

# 참고 자료

- Docker Official Documentation

https://docs.docker.com/

- Docker Hub

https://hub.docker.com/

- Git Official Documentation

https://git-scm.com/doc

- Nginx Official Documentation

https://nginx.org/