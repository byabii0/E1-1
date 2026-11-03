# E1-1
# 프로젝트 개요

📌 한 줄 요약

터미널 환경 정리부터 Docker 컨테이너 실행·관리까지, "왜 이런 설계가 필요한가"를 스스로 설명할 수 있는 수준으로 끌어올리는 실습 프로젝트입니다.

🎯 학습 목표

단순히 명령어를 따라 치는 것이 아니라, 실행 결과로 원리를 직접 눈으로 확인하고 설명할 수 있는 것이 핵심입니다.
"내 컴퓨터에서만 돌아가는 문제"를 없애고, 팀원 누구나 같은 방식으로 실행 · 배포 · 디버깅 할 수 있는 환경을 직접 구성합니다.

✅ 미션 완료 체크리스트

📁 터미널 & 리눅스 기초

- [ ] 절대 경로 vs 상대 경로 차이를 예시로 설명할 수 있다.
- [ ] 파일 권한(r/w/x) 의미와 755, 644 표기를 해석할 수 있다.

🐳 Docker 핵심

- [ ] 기존 Dockerfile을 기반으로 커스텀 이미지를 만들 수 있다.
- [ ] 포트 매핑이 필요한 이유를 설명할 수 있다.
- [ ] Docker 볼륨(영속 데이터)을 설명할 수 있다.

🤝 협업 도구

- [ ] Git vs GitHub 역할 차이를 설명할 수 있다.
Git = 로컬 버전 관리
GitHub = 원격 협업 플랫폼

# 실행 환경
OS 버전: Microsoft Windows 버전 26H2(OS 빌드 26300.9711)

쉘 버전: PS 5.1.26100.9711

터미널 버전: VS Code terminal v1.144.0.0

Docker 버전: 29.9.2

Git 버전: 2.56.0.windows.4

# 수행 항목 체크리스트

터미널/권한: 터미널 조작 로그

- [ ] 터미널에서 수행한 핵심 명령과 출력 결과를 기술 문서에 기록한다.

Docker: Docker 운영/검증 로그

- [ ] docker --version, docker info 등 설치·점검 결과
- [ ] docker images, docker ps -a, docker logs, docker stats 등 운영 명령 실행 흔적

Dockerfile: Dockerfile 기반 웹 서버 컨테이너

- [ ] 웹 서버 소스코드(예: app/ 또는 src/)
- [ ] Dockerfile
- [ ] 빌드/실행 명령 및 결과 로그(터미널 스크린샷 가능)
- [ ] 포트 매핑 접속 성공 증거(스크린샷 또는 로그)

포트: 포트 매핑 접속 증거
- [ ] p <host_port>:<container_port>로 실행 후, 브라우저 접속 화면(주소창 포함)을 기술 문서에 첨부한다.

볼륨: 바인드 마운트 반영 + 볼륨 영속성 증거
- [ ] 바인드 마운트: 실행 명령 + 호스트 변경 전/후 비교
- [ ] Docker 볼륨: 생성/연결/검증 명령 + 컨테이너 삭제 전/후 비교

Git/GitHub: Git 설정 및 GitHub/VSCode 연동 증거

- [ ] Git 사용자 정보·기본 브랜치 설정 후, VSCode에서 GitHub 로그인 및 저장소 연동 완료
- [ ] 민감한 개인 정보(ID/PW, 토큰 등)가 포함되지 않도록 주의한다.

# 터미널 조작 로그

터미널에서 수행한 핵심 명령

위치 확인 및 이동: pwd, cd

PS C:\test\집> cd ~
PS C:\Users\kmj04> pwd

Path          
----          
C:\Users\kmj04

폴더와 파일 만들기: mkdir, touch

목록 확인하기: ls, ls -l, ls -a, ls -la, tree

권한 정리: chmod

파일 내용 작성 및 실행: cat, bash

# 검증 방법(어떤 명령으로 무엇을 확인했는지)+결과 위치 링크

실행 환경

OS 환경 상세: PS C:\WINDOWS\system32> winver

통합:

$os = Get-CimInstance Win32_OperatingSystem
$ver = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion').DisplayVersion
Write-Host "OS: $($os.Caption) (버전 $ver, OS 빌드 $($os.BuildNumber)) | Shell: PS $($PSVersionTable.PSVersion) | Terminal: $(if ($env:TERM_PROGRAM -eq 'vscode') {"VSCode Terminal v$env:TERM_PROGRAM_VERSION"} elseif ($env:WT_SESSION) {'Windows Terminal'} else {$Host.Name}) | Docker: $(docker --version) | Git: $(git --version)"

OS: Microsoft Windows 11 Pro (버전 26H2, OS 빌드 26300) | Shell: PS 5.1.26100.9711 | Terminal: VSCode Terminal v1.144.0 | Docker: Docker version 29.9.2, build a82e528 | Git: git version 2.56.0.windows.4

---


# 트러블슈팅 2건 이상(문제 → 원인 가설 → 확인 → 해결/대안)

# 터미널 조작 로그-터미널에서 수행한 핵심 명령과 출력 결과를 기술 문서에 기록한다.

# Docker 운영/검증 로그

# Dockerfile 기반 웹 서버 컨테이너

# 포트 매핑 접속 증거

# 바인드 마운트 반엉 + 볼륨 영속성 증거

# Git 설정 및 GitHub/VSCode 연동 증거
