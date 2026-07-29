# 1. 베이스 이미지 선택 - 경량 모델 이미지 
FROM nginx:alpine


# 2. 작업 디렉토리 설정 
# 이후의 COPY나 RUN은 모두 이 폴더 기준으로 동작  
WORKDIR /usr/share/nginx/html

# 3. 환경 변수 및 라벨
ENV APP_OWNER="BalsamNCedar"
ENV APP_STATUS="Learning"

LABEL maintainer="balsamncedar56301@c5r8s4"
LABEL description="기본 Nginx 페이지를 커스텀 페이지로 교체"

# 4. 패키지 설치 (내부 도구 추가)
RUN apk update && apk add curl

# 5. 정적 컨텐츠 교체  
# WORKDIR을 설정했으므로, 목적지 경로를 짧게 사용가능
COPY index.html ./index.html


# 6. C : 헬스체크 추가 - 컨테이너 상태 감시
# cur -f (fail)
HEALTHCHECK --interval=30s --timeout=3s \ 
    CMD curl -f http://localhost/ || exit 1

# (참고) NginX는 기본적으로 80 포트사용
EXPOSE 80