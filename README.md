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
├── README.md          # 본 문서
├── .gitignore         # Git 제외 목록
├── Dockerfile         # 환경 재현을 위한 도커 설정
├── logs/              # 수행 과정 로그 모음 (.log)
├── images/            # 결과 증빙 스크린샷 (.png, .jpg)
├── practice/          # 터미널 실습용 디렉토리
└── site/              # 결과물 저장소
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

## 6. 트러블슈팅 (Troubleshooting)

### Case 1: 
- **문제** : 
- **원인 가설**:
0 **해결**:

### Case 2:
