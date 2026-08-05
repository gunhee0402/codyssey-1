# 1. 베이스 이미지 선택 (이미 만들어진 Nginx라는 컴퓨터를 빌려옵니다)
FROM nginx:latest

# 2. 내가 만든 index.html 파일을 Nginx가 웹 페이지를 보여주는 기본 경로로 복사합니다
COPY index.html /usr/share/nginx/html/index.html

# 3. 이 컨테이너는 80번 포트(웹 서비스 기본 통로)를 사용할 거라고 알려줍니다
EXPOSE 80