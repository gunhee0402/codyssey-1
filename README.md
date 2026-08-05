# 🐳 Docker 기반 정적 웹 서버 구축 프로젝트

비전공자로서 도커의 핵심 개념(이미지, 컨테이너, 포트 매핑, 볼륨)을 학습하기 위한 프로젝트입니다.

## 🛠 사용 기술
- **Docker** / **Docker Compose**
- **Nginx** (Web Server)
- **HTML/CSS**

## 🚀 실행 방법
1. 저장소 클론: `git clone https://github.com/본인아이디/codyssey-1.git`
2. 컨테이너 실행: `docker-compose up -d`
3. 접속: `http://localhost:8081`

## 💡 주요 학습 내용
- **포트 매핑**: 호스트의 8081 포트를 컨테이너의 80 포트와 연결하여 외부 접속 허용.
- **볼륨(Volume)**: 호스트의 폴더와 컨테이너 내부 경로를 동기화하여 코드 수정 시 즉시 반영되도록 설정.
- **Docker Compose**: 복잡한 도커 명령어를 파일로 관리하여 실행 프로세스 간소화.