# E1-1 Linux CLI / Docker / Git 실습

## 프로젝트 소개

Codyssey E1-1 미션입니다.

이번 미션에서는 Linux CLI, 파일 권한, Docker, Dockerfile, Volume, Port Mapping, Git, GitHub를 직접 실습하며 기본적인 개발환경을 구축하는 것을 목표로 합니다.

---

# 목차

1. 프로젝트 목표
2. 개발환경
3. 프로젝트 구조
4. 수행 내용
5. Linux CLI 실습
6. 파일 권한 실습
7. Docker 설치 및 실행
8. Dockerfile 작성
9. Docker Container 실행
10. Docker Volume
11. Docker Compose
12. Git & GitHub
13. 느낀점

---

# 1. 프로젝트 목표

이번 프로젝트를 통해 아래 내용을 직접 수행하였습니다.

- Linux Terminal 사용
- 파일 생성 및 관리
- 파일 권한 변경
- Docker 설치
- Docker Image Build
- Docker Container 실행
- Docker Volume
- Docker Compose
- GitHub Repository 관리

---

# 2. 개발환경

|항목|내용|
|---|---|
|OS|Windows11 + WSL2|
|Terminal|Git Bash|
|IDE|Visual Studio Code|
|Docker|29.6.2|
|Git|Git for Windows|
|Repository|GitHub|

---

# 3. 프로젝트 구조

```text
codyssey-1
│
├── README.md
│
└── practice
    │
    ├── Dockerfile
    ├── docker-compose.yml
    ├── index.html
    └── test.txt
```

> 프로젝트 구조는 실습 과정에 따라 일부 변경될 수 있습니다.

---

# 4. 수행 내용

이번 프로젝트에서는 다음 순서대로 진행했습니다.

1. Linux CLI 실습

2. 파일 권한 변경

3. Docker 설치 확인

4. Hello World 실행

5. Docker Image Build

6. Docker Container 실행

7. Port Mapping

8. Docker Volume

9. Docker Compose

10. GitHub 업로드

---

# 5. Linux CLI 실습

## 5-1 현재 위치 확인

현재 작업중인 위치를 확인합니다.

```bash
pwd
```

실행 결과

```bash
/c/Users/jkhlm/codyssey-1
```

📷 스크린샷 첨부

---

## 5-2 practice 폴더 생성

```bash
mkdir practice
```

생성 후 practice 디렉토리로 이동합니다.

```bash
cd practice
```

실행 결과

```bash
jkhlm@... ~/codyssey-1/practice (main)
```

📷 스크린샷 첨부

---

## 5-3 파일 생성

빈 파일(test.txt)을 생성합니다.

```bash
touch test.txt
```

생성된 파일을 확인합니다.

```bash
ls -la
```

실행 결과

```bash
total 0

drwxr-xr-x

-rw-r--r--

test.txt
```

📷 스크린샷 첨부

---

## 5-4 파일 권한 확인

```bash
ls -l test.txt
```

실행 결과

```bash
-rw-r--r-- test.txt
```

Linux에서는

r = Read

w = Write

x = Execute

권한을 의미합니다.
---

# 6. 파일 권한(Permission) 실습

Linux에서는 모든 파일과 디렉터리에 대해 접근 권한(Permission)이 존재합니다.

권한은 아래 3가지로 구성됩니다.

|권한|의미|
|---|---|
|r|Read (읽기)|
|w|Write (쓰기)|
|x|Execute (실행)|

권한은 사용자(User), 그룹(Group), 기타 사용자(Other)에게 각각 부여됩니다.

---

## 6-1 현재 권한 확인

먼저 생성한 test.txt의 권한을 확인하였습니다.

실행 명령

```bash
ls -l test.txt
```

실행 결과

```bash
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

권한과 동일합니다.

|사용자|권한|
|---|---|
|Owner|Read + Write|
|Group|Read|
|Other|Read|

📷 **스크린샷 첨부**

---

## 6-2 chmod 명령어 사용

이번에는 chmod를 이용하여 권한을 변경하였습니다.

실행 명령

```bash
chmod 755 test.txt
```

권한 변경 후 다시 확인합니다.

```bash
ls -l test.txt
```

실행 결과

```bash
-rwxr-xr-x
```

755는 아래와 같은 의미입니다.

|숫자|권한|
|---|---|
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

권한만 갖습니다.

📷 **스크린샷 첨부**

---

# 7. Docker 설치 확인

Docker Desktop 설치가 정상적으로 완료되었는지 확인하였습니다.

---

## 7-1 Docker Version 확인

실행 명령

```bash
docker --version
```

실행 결과

```bash
Docker version 29.6.2, build dfc4efb
```

현재 Docker가 정상적으로 설치되어 있으며 CLI에서도 사용할 수 있음을 확인하였습니다.

📷 **스크린샷 첨부**

---

## 7-2 Docker 정보 확인

Docker Engine이 정상적으로 실행되는지 확인하기 위해 아래 명령을 실행하였습니다.

```bash
docker info
```

실행 결과

```text
Client:

Version: 29.6.2

Context: desktop-linux

Plugins:

agent

buildx

compose

desktop

...

Server:

Containers: 0

Running: 0

Stopped: 0

Images: 1

Storage Driver: overlayfs

Operating System: Docker Desktop

Architecture: x86_64

CPUs: 8

Total Memory: 7.527GiB

Docker Root Dir: /var/lib/docker

...
```

Docker Client와 Docker Server 모두 정상적으로 실행되고 있는 것을 확인할 수 있었습니다.

또한 Docker Desktop에서 WSL2 기반으로 동작하는 것도 확인되었습니다.

📷 **스크린샷 첨부**

---

# 8. Hello World 실행

Docker 설치가 정상적으로 완료되었는지 확인하기 위해 Hello World 이미지를 실행하였습니다.

---

## 8-1 hello-world 실행

실행 명령

```bash
docker run hello-world
```

처음 실행하는 이미지이기 때문에 Docker Hub에서 자동으로 이미지를 다운로드하였습니다.

실행 결과

```text
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

Docker Hub에서 이미지를 다운로드한 뒤 컨테이너를 생성하고 정상적으로 실행되는 것을 확인하였습니다.

이를 통해 Docker Engine이 정상적으로 동작하는 것을 확인할 수 있었습니다.

📷 **스크린샷 첨부**

---

## 학습 내용

이번 실습을 통해 다음 내용을 이해할 수 있었습니다.

- Docker는 이미지(Image)를 기반으로 컨테이너(Container)를 생성한다.
- 이미지가 존재하지 않으면 Docker Hub에서 자동으로 다운로드한다.
- hello-world 이미지는 Docker 설치 확인용으로 가장 많이 사용된다.
- Docker Client와 Docker Daemon이 서로 통신하여 컨테이너를 실행한다.
---

# 9. Dockerfile 작성

이번 실습에서는 Nginx 공식 이미지를 기반으로 커스텀 이미지를 생성하였습니다.

Dockerfile을 직접 작성하여 웹 페이지를 컨테이너 내부에 복사하고, 이를 Docker Image로 빌드하였습니다.

---

## 9-1 Dockerfile 작성

작성한 Dockerfile은 아래와 같습니다.

```Dockerfile
FROM nginx:latest

COPY index.html /usr/share/nginx/html/index.html
```

---

### 코드 설명

#### FROM nginx:latest

```Dockerfile
FROM nginx:latest
```

Docker Hub에 등록되어 있는 공식 nginx 이미지를 베이스 이미지로 사용합니다.

nginx는 웹 서버 역할을 수행하며 기본적으로 80번 포트를 사용합니다.

---

#### COPY

```Dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

현재 프로젝트 폴더에 존재하는

```
index.html
```

파일을

```
/usr/share/nginx/html/
```

경로로 복사합니다.

해당 디렉터리는 nginx가 기본적으로 웹 페이지를 제공하는 위치입니다.

컨테이너가 실행되면 브라우저에서 localhost:8080으로 접속하여 이 파일을 확인할 수 있습니다.

📷 **Dockerfile 작성 화면**

---

# 10. Docker Image Build

Dockerfile을 이용하여 Docker 이미지를 생성하였습니다.

---

## 10-1 첫 번째 Build (실패)

처음에는 Dockerfile이 비어있는 상태에서 Build를 진행하였습니다.

실행 명령

```bash
docker build -t my-web-server .
```

실행 결과

```text
[+] Building 0.4s (1/1) FINISHED

ERROR: failed to build: failed to solve:

the Dockerfile cannot be empty
```

---

### 원인 분석

Docker Build는 현재 폴더의 Dockerfile을 읽어서 이미지를 생성합니다.

하지만 Dockerfile 내부가 비어 있었기 때문에 Build를 수행할 수 없었습니다.

Docker는 어떤 이미지를 사용할지,

어떤 파일을 복사할지,

어떤 명령을 실행해야 하는지 알 수 없어 오류가 발생했습니다.

---

### 해결 방법

Dockerfile을 작성한 후 다시 Build를 수행하였습니다.

📷 **실패 화면 첨부**

---

## 10-2 Docker Build 성공

Dockerfile을 수정한 후 다시 Build를 진행하였습니다.

실행 명령

```bash
docker build -t my-web-server .
```

실행 결과

```text
[+] Building 3.5s (8/8) FINISHED

=> [internal] load build definition

=> [internal] load metadata

=> [internal] load .dockerignore

=> [internal] load build context

=> [1/2] FROM docker.io/library/nginx:latest

=> [2/2] COPY index.html /usr/share/nginx/html/index.html

=> exporting to image

=> naming to docker.io/library/my-web-server

=> unpacking to docker.io/library/my-web-server
```

Dockerfile을 정상적으로 읽어 Docker 이미지를 생성하였습니다.

Build 과정에서는

- Dockerfile 로드
- nginx 이미지 다운로드
- Build Context 업로드
- index.html 복사
- 이미지 생성

순서로 진행되었습니다.

📷 **Build 성공 화면**

---

## Build 과정 이해

Docker Build는 아래 순서대로 수행됩니다.

1. Dockerfile 읽기

2. Base Image 다운로드

3. Build Context 업로드

4. Dockerfile 명령 실행

5. Image 생성

이번 프로젝트에서는 총 2개의 Layer가 생성되었습니다.

### Layer 1

```Dockerfile
FROM nginx:latest
```

nginx 공식 이미지를 기반으로 합니다.

---

### Layer 2

```Dockerfile
COPY index.html /usr/share/nginx/html/index.html
```

웹 페이지를 컨테이너 내부로 복사합니다.

---

## 생성된 이미지

Build가 완료되면

```
my-web-server
```

라는 이름의 이미지가 생성됩니다.

이 이미지를 이용하여 여러 개의 컨테이너를 실행할 수 있습니다.

📷 **Docker Images 화면 첨부**
---

# 11. Docker Container 실행

Docker Image Build가 완료된 후 생성된 이미지를 이용하여 컨테이너를 실행하였습니다.

Docker에서는 하나의 이미지를 이용하여 여러 개의 컨테이너를 생성할 수 있습니다.

이번 실습에서는 Nginx 기반 웹 서버를 실행하고, 포트 매핑 및 컨테이너 관리 명령어를 직접 수행하였습니다.

---

## 11-1 컨테이너 실행

실행 명령

```bash
docker run -d -p 8080:80 --name my-first-container my-web-server
```

실행 결과

```text
b618cae534da50ff614ce28e609875ed07bfd10afef2a9a9ff3d79fa65e1c561
```

### 명령어 설명

|옵션|설명|
|---|---|
|-d|백그라운드 실행|
|-p 8080:80|호스트의 8080 포트를 컨테이너의 80 포트와 연결|
|--name|컨테이너 이름 지정|

즉,

브라우저에서

```
http://localhost:8080
```

으로 접속하면 nginx가 제공하는 웹 페이지를 확인할 수 있습니다.

📷 **컨테이너 실행 화면 첨부**

---

## 11-2 실행 중인 컨테이너 확인

컨테이너가 정상적으로 실행되고 있는지 확인하기 위해 아래 명령을 실행하였습니다.

```bash
docker ps
```

실행 결과

```text
CONTAINER ID   IMAGE           COMMAND                   CREATED          STATUS          PORTS                                     NAMES
b618cae534da   my-web-server   "/docker-entrypoint.…"   49 seconds ago   Up 48 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   my-first-container
```

실행 중인 컨테이너의 정보를 확인할 수 있었습니다.

확인 가능한 정보

- Container ID
- Image 이름
- 실행 시간
- 상태(Status)
- Port Mapping
- Container Name

📷 **docker ps 결과 첨부**

---

## 11-3 컨테이너 종료

실행 명령

```bash
docker stop my-first-container
```

실행 결과

```text
my-first-container
```

Container를 정상적으로 종료하였습니다.

---

## 11-4 컨테이너 삭제

실행 명령

```bash
docker rm my-first-container
```

실행 결과

```text
my-first-container
```

종료된 컨테이너를 삭제하였습니다.

Docker에서는 실행 중인 컨테이너는 삭제할 수 없으며,

반드시 Stop 후 Remove를 수행해야 합니다.

📷 **Stop / Remove 화면 첨부**

---

# 12. Docker Volume (Bind Mount)

Docker에서는 컨테이너가 삭제되면 내부 데이터도 함께 삭제됩니다.

이를 해결하기 위해 Host와 Container를 연결하는 Bind Mount를 실습하였습니다.

---

## 12-1 첫 번째 Bind Mount

실행 명령

```bash
docker run -d -p 8080:80 -v $(pwd)/index.html:/usr/share/nginx/html/index.html --name volume-test my-web-server
```

실행 결과

```text
b93b8e828e0a6cb524470f683a0df5f4998b7d4712edd80b980739f11919e788
```

Host의

```
index.html
```

파일을

Container 내부

```
/usr/share/nginx/html/index.html
```

에 연결하였습니다.

즉,

Host에서 index.html을 수정하면

Container 내부에서도 즉시 반영됩니다.

📷 **Bind Mount 화면 첨부**

---

## 12-2 컨테이너 종료

```bash
docker stop volume-test
```

실행 결과

```text
volume-test
```

---

## 12-3 컨테이너 삭제

```bash
docker rm volume-test
```

실행 결과

```text
volume-test
```

---

## 12-4 프로젝트 전체 마운트

이번에는 프로젝트 폴더 전체를 Mount 하였습니다.

실행 명령

```bash
docker run -d -p 8081:80 -v "/$(pwd):/usr/share/nginx/html" --name volume-test my-web-server
```

실행 결과

```text
a692222b4e3f82f19a1df02c81f8c700f0c258b7e58e8f2fbb0060345f474eca
```

Host의 현재 디렉터리를 Container의 웹 루트와 연결하였습니다.

따라서 프로젝트 내 HTML 파일을 수정하면 컨테이너를 다시 Build하지 않아도 변경사항을 바로 확인할 수 있습니다.

📷 **전체 폴더 Mount 화면 첨부**

---

## 12-5 입력 오류 발생

실습 중 터미널에 잘못된 문자열이 입력되는 오류가 발생하였습니다.

실행 결과

```text
$ [200~docker stop volume-test~

bash:

[200~docker:

command not found
```

### 원인

터미널에 붙여넣는 과정에서 특수문자가 함께 입력되었습니다.

### 해결

명령어를 다시 입력하여 정상적으로 종료하였습니다.

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

명령을 실행하여 정상적으로 삭제하였습니다.

📷 **오류 및 해결 화면 첨부**

---

## 이번 실습에서 배운 점

- 하나의 이미지는 여러 개의 컨테이너를 생성할 수 있다.
- Port Mapping을 이용하여 Host와 Container를 연결할 수 있다.
- docker ps 명령으로 실행 상태를 확인할 수 있다.
- docker stop 명령으로 실행 중인 컨테이너를 종료할 수 있다.
- docker rm 명령으로 컨테이너를 삭제할 수 있다.
- Bind Mount를 이용하면 Host와 Container가 동일한 파일을 공유할 수 있다.
- Build를 다시 수행하지 않아도 HTML 수정 내용이 즉시 반영된다.