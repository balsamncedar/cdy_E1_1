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

- [x] 리다이렉션 및 파이프라인 활용

- [x] Docker 설치 및 컨테이너 실행

- [ ] Dockerfile 작성 및 이미지 빌드

- [ ] Git 로컬 저장소 생성 및 GitHub 원격 연결

  

## 5. 검증 방법 및 결과

| 항목 | 검증 방법 | 결과 링크 |

| :--- | :--- | :--- |

| 터미널 실습 | `ls -al` 명령어로 구조 확인 | [로그 확인](./logs/terminal_practice.log) |

| Docker 실행 | `docker ps` 결과 확인 | [스크린샷](./images/docker_result.png) |

  
-------

 ###  터미널 명령어
#### 1. 현재 위치
```bash
$ pwd
```
 
 ```bash
#출력 결과 :
/Users/balsamncedar56301/Desktop/cdy-suz/mission1
```
* 이미지
![pwd 화면캡쳐](./images/pwd_capture.png) 
  

#### 2. 파일 목록 

```bash
$ ls -al
```
```bash
total 8
drwxr-xr-x  6 balsamncedar56301  balsamncedar56301  192 Jul 27 19:37 .
drwxr-xr-x  3 balsamncedar56301  balsamncedar56301 96 Jul 27 19:22 ..
-rw-r--r--  1 balsamncedar56301  balsamncedar56301  476 Jul 27 19:32 README.md
drwxr-xr-x  3 balsamncedar56301  balsamncedar56301 96 Jul 27 19:52 logs
drwxr-xr-x  5 balsamncedar56301  balsamncedar56301  160 Jul 27 19:42 practice
drwxr-xr-x  2 balsamncedar56301  balsamncedar56301 64 Jul 27 19:34 site
```
  
* 이미지 
![list all 화면캡쳐](./images/list.png)
  

####  3. 파일 생성 및 복사,  결과 확인 

```bash
$ touch memo.txt
$ echo "Hello Terminal" >> memo.txt
$ cp practice/memo.txt practice/memo_backup.txt
$ cat memo_backup.txt
```
  
``` bash
#출력 결과 :
Hello Terminal
```
* 이미지
![touch copy read file](./images/mkcpcat.png)



####  4. 파일 이동 및 이름 변경 

```bash
$ ls 
$ mv memo_backup.txt ../site/moved_memo.txt
$ cd ../site/
$ ls -al
```
  
  
* 이미지
![move file and rename](./images/mvrename.png)  

  

#### 5. 파일 삭제
```bash
$ rm  site/moved_memo.txt
$ ls -al
```
  
* 이미지
![remove file](./images/removefile.png)


####  6. 빈파일 생성및 파일 내용확인 

```bash
$ touch sample.txt
$ ls 
$ echo "This is sample text"  >> sample.txt
$ cat sample.txt
```
  
* 이미지
![make file and read file](./images/makefileAndRead.png)
  

#### 7. 권한 실습(확인 및 변경)

```bash
$ touch  secret.txt
$ echo "my-password-1234" >> secret.txt
$ ls -al
$ chmod 000 secret.txt
$ cat secret.txt
$ chmod 777 secret.txt
$ cat secret.txt

```

* 이미지
![chmod](./images/chmod.png)


 
## 6. 트러블슈팅 (Troubleshooting)

  

### Case 1:

- **문제** :

- **원인 가설**:

0 **해결**:

  

### Case 2
