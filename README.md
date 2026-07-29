# 개발 워크스테이션 구축 프로젝트

  

이 프로젝트는 터미널, Docker, Git을 활용하여 재현 가능한 개발 환경을 구축하는 과정을 기록합니다.

  

## 1. 실행 환경

- **OS**: macOS 15.7.4

- **Shell**: /bin/zsh

- **Docker**: Docker version 28.5.2, build ecc6942

- **Git**: git version 2.53.0

  

## 2. 프로젝트 구조

  

```text

mission1/

├── README.md  # 본 문서

├── .gitignore # Git 제외 목록

├── Dockerfile # 환경 재현을 위한 도커 설정

├── logs/  # 수행 과정 로그 모음 (.log)

├── images/  # 결과 증빙 스크린샷 (.png, .jpg)

├── practice/  # 터미널 실습용 디렉토리

└── site/  # 결과물 저장소

```

  

  

## 4. 수행 항목 체크리스트

- [x] 터미널 기본 명령어 숙달 (`ls`, `cd`, `mkdir`, `rm` 등)

- [x] 권한 실습 (chmod) 및 파일 보안 확인

- [x] Docker 설치 및 데몬 동작 확인

- [x] Docker 기본 명령 (images, ps, logs, stats)

- [ ] Ubuntu 컨테이너 진입 및 attach/exec 차이 이해

- [ ] Dockerfile 작성 및 이미지 빌드

- [ ] 포트 포워딩 및 브라우저 접속 확인

- [ ] Docker 볼륨을 이용한 데이터 영속성 검증

- [ ] Git 로컬 저장소 생성 및 GitHub 원격 연결

  

## 5. 검증 방법 및 결과 요약
| 항목 | 검증 방법 | 결과 위치 |
| :--- | :--- | :--- |
| 터미널 실습 | 명령어 수행 및 파일 이동 확인 | [5.1 터미널 로그](#51-터미널-조작-로그) |
| 권한 실습 | `chmod 000` 후 접근 거부 확인 | [5.2 권한 실습](#52-권한-실습) |
| Docker 기본 | `version`, `info` 확인 | [6.1 Docker 점검](#61-docker-설치-및-기본-점검) |
| 컨테이너 실습 | `hello-world`, `ubuntu` 실행 | [6.2 컨테이너 실습](#62-컨테이너-실행-실습) |
| 커스텀 이미지 | Dockerfile 빌드 및 접속 | (작성 예정) |
| 볼륨 영속성 | 컨테이너 삭제 후 데이터 확인 | (작성 예정) |
| Git 설정 | `git config --list` 확인 | (작성 예정) |


-------

## 5. 터미널 및 권한 실습 상세

### 5.1 터미널 조작 로그
#### 1. 현재 위치
```bash
$ pwd
```

* 출력결과
![pwd 현재 위치(작업폴더)](./images/pwd_capture.png)
  

#### 2. 파일 목록 

```bash
$ ls -al
```
  
* 출력결과 
![list all 화면캡쳐](./images/listall.png)
  

####  3. 파일 생성 및 복사,  결과 확인 

```bash
$ touch memo.txt
$ echo "Hello Terminal" >> memo.txt
$ cp practice/memo.txt practice/memo_backup.txt
$ cat memo_backup.txt
```
  
* 출력결과
![touch copy read file](./images/mkcpcat.png)



####  4. 파일 이동 및 이름 변경 

```bash
$ ls 
$ mv memo_backup.txt ../site/moved_memo.txt
$ cd ../site/
$ ls -al
```
  
  
* 출력결과
![move file and rename](./images/mvrename.png)  

  

#### 5. 파일 삭제
```bash
$ rm  site/moved_memo.txt
$ ls -al
```
  
* 출력결과
![remove file](./images/removefile.png)


####  6. 빈파일 생성및 파일 내용확인 

```bash
$ touch sample.txt
$ ls 
$ echo "This is sample text"  >> sample.txt
$ cat sample.txt
```
  
* 출력결과
![make file and read file](./images/makefileAndRead.png)
  

### 5.2 권한 실습

```bash
$ touch  secret.txt
$ echo "my-password-1234" >> secret.txt
$ ls -al
$ chmod 000 secret.txt
$ cat secret.txt
$ chmod 777 secret.txt
$ cat secret.txt

```

* 출력결과
![chmod](./images/chmod.png)


---

## 6. Docker 운영 실습

### 6.1 Docker 설치 및 기본 점검
- **버전 확인**: `docker --version`
- **데몬 상태**: `docker info` (또는 OrbStack 대시보드 확인)
- **이미지 다운 목록 확인 ** : `docker images` 
   ![docker images](./images/dockerImages.png)
- **로그 확인 ** :  `docker logs`
    ![docker logs](./images/dockerLogs.png)
    ![docker logs](./images/monitoringLogsInRealtime.png)

- **리소스 확인 ** : `docker stats`
    ```bash
    docker stats test-nginx
    ```
    ![docker stats](./images/dockerStats.png)

### 6.2 컨테이너 실행 실습
1. **hello-world**: `docker run hello-world` 성공 기록
2. **Ubuntu 진입**:
   ```bash
   docker run -it --name my-ubuntu ubuntu bash
   # 내부에서 ls, echo 수행
   ```
3. **관찰 결과 (attach vs exec)**:
   - `attach`: 메인 프로세스에 연결되어 `exit` 시 컨테이너 종료됨.
   ![docker attach](./images/dockerAttach.png)
   
   - `exec`: 새로운 세션을 열어 `exit` 해도 컨테이너가 유지됨.
    ![docker exec](./images/execTestNginX.png)
---

## 7. 커스텀 이미지 제작 (진행 예정)
    - 작업 순서 : docker 파일 작성 -> 빌드 -> 띄운 위치로 웹에서 확인 
    - 비교 방향 : 커스텀 이미지와 기본 이미지 비교
    ```bash
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
    ```
    ```bash
        # 만든 도커이미지 빌드
        docker build -t my_custom_nginix:v1 .
    ```

    - 컨테이너에  (커스텀이미지 - 8888에 매핑 ) vs  (기본 이미지 - 8080 에 매핑)
    ```bash
    docker run -d -p 8888:80 --name custom_web my-custom-nginx:v1

    docker run -d -p 8080:80 --name original-web nginx:alptine
    ```
* 출력결과
![커스텀이미지_my_custom_nginx:v1](../cdy_E1_1/images/custom_web_img.png)
![기본이미지_nginx:alpine](../cdy_E1_1/images/original_web_8080.png)

    - 이미지의 메타 데이터를 확인하고 싶을때
    ```bash
    docker inspect my-custom-nginx:v1 

    docker inspect my-custom-nginx:v1 --formt='{{json .Config.Env}}' | python3 -m json.tool 
    inspect my-custom-nginx:v1 --format='{{json .Config.Labels}}' | python3 -m json.tool

    ```

* 출력 결과
![docker inspect 전체](../cdy_E1_1/images/docker-insepct.png)
![docker inspect 부분](../cdy_E1_1/images/docker-inspect-Labels.png)

    - curl 로 확인하기 
    ```bash
    # docker 주소
    # 출력 결과 html 
    curl localhost:8080

    # 돌아가고 있는지 HTTP 응답값 줌 
    curl -I localhost:8080 
    
    ```
* 출력 결과
![curl 응답으로 확인하기](../cdy_E1_1/images/curl_originalWeb.png)    

## 8. Docker 볼륨 및 데이터 영속성 (진행 예정)
*(이후 진행될 볼륨 실습 내용을 여기에 작성)*




## 9. Git 및 GitHub 연동 (진행 예정)
*(이후 진행될 Git 설정 내용을 여기에 작성)*

## 10. 트러블슈팅 (Troubleshooting)
### Case 1: (예시) 권한 문제
- **문제**: `sudo` 없이 docker 명령어가 안 먹히는 현상
- **원인**: 사용자 그룹 설정 미비
- **해결**: OrbStack 설정 확인 또는 유저 그룹 추가

---