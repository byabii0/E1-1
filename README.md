# E1-1
# 프로젝트 개요

📌 한 줄 요약

터미널 환경 정리부터 Docker 컨테이너 실행·관리까지, "왜 이런 설계가 필요한가"를 스스로 설명할 수 있는 수준으로 끌어올리는 실습 프로젝트입니다.

🎯 학습 목표

단순히 명령어를 따라 치는 것이 아니라, 실행 결과로 원리를 직접 눈으로 확인하고 설명할 수 있는 것이 핵심입니다.
"내 컴퓨터에서만 돌아가는 문제"를 없애고, 팀원 누구나 같은 방식으로 실행 · 배포 · 디버깅 할 수 있는 환경을 직접 구성합니다.

✅ 미션 완료 체크리스트

📁 터미널 & 리눅스 기초

- [x] 절대 경로 vs 상대 경로 차이를 예시로 설명할 수 있다.
- [x] 파일 권한(r/w/x) 의미와 755, 644 표기를 해석할 수 있다.

🐳 Docker 핵심

- [x] 기존 Dockerfile을 기반으로 커스텀 이미지를 만들 수 있다.
- [x] 포트 매핑이 필요한 이유를 설명할 수 있다.
- [x] Docker 볼륨(영속 데이터)을 설명할 수 있다.

🤝 협업 도구

- [x] Git vs GitHub 역할 차이를 설명할 수 있다.
Git = 로컬 버전 관리
GitHub = 원격 협업 플랫폼

# 실행 환경
OS 버전: Microsoft Windows 버전 26H2(OS 빌드 26300.9711)

쉘 버전: PS 5.1.26100.9711

터미널 버전: VS Code terminal v1.144.0.0

Docker 버전: 29.9.2

Git 버전: 2.56.0.windows.4

OS 환경 상세

        PS C:\WINDOWS\system32> winver

실행 환경 확인 코드 통합

        $os = Get-CimInstance Win32_OperatingSystem
        $ver = (Get-ItemProperty 'HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion').DisplayVersion
        Write-Host "OS: $($os.Caption) (버전 $ver, OS 빌드 $($os.BuildNumber)) | Shell: PS $($PSVersionTable.PSVersion) | Terminal: $(if ($env:TERM_PROGRAM -eq 'vscode') {"VSCode Terminal v$env:TERM_PROGRAM_VERSION"} elseif ($env:WT_SESSION) {'Windows Terminal'} else {$Host.Name}) | Docker: $(docker --version) | Git: $(git --version)"
            
        OS: Microsoft Windows 11 Pro (버전 26H2, OS 빌드 26300) | Shell: PS 5.1.26100.9711 | Terminal: VSCode Terminal v1.144.0 | Docker: Docker version 29.9.2, build a82e528 | Git: git version 2.56.0.windows.4

# 수행 항목 체크리스트

터미널/권한: 터미널 조작 로그

- [x] 터미널에서 수행한 핵심 명령과 출력 결과를 기술 문서에 기록한다.

Docker: Docker 운영/검증 로그

- [x] docker --version, docker info 등 설치·점검 결과
- [x] docker images, docker ps -a, docker logs, docker stats 등 운영 명령 실행 흔적

Dockerfile: Dockerfile 기반 웹 서버 컨테이너

- [x] 웹 서버 소스코드(예: app/ 또는 src/)
- [x] Dockerfile
- [x] 빌드/실행 명령 및 결과 로그(터미널 스크린샷 가능)
- [x] 포트 매핑 접속 성공 증거(스크린샷 또는 로그)

포트: 포트 매핑 접속 증거
- [x] p <host_port>:<container_port>로 실행 후, 브라우저 접속 화면(주소창 포함)을 기술 문서에 첨부한다.

볼륨: 바인드 마운트 반영 + 볼륨 영속성 증거
- [x] 바인드 마운트: 실행 명령 + 호스트 변경 전/후 비교
- [x] Docker 볼륨: 생성/연결/검증 명령 + 컨테이너 삭제 전/후 비교

Git/GitHub: Git 설정 및 GitHub/VSCode 연동 증거

- [x] Git 사용자 정보·기본 브랜치 설정 후, VSCode에서 GitHub 로그인 및 저장소 연동 완료
- [x] 민감한 개인 정보(ID/PW, 토큰 등)가 포함되지 않도록 주의한다.

# 터미널 조작 로그

위치 확인 및 이동: pwd, cd

    PS C:\test\집> cd ~
    PS C:\Users\kmj04> pwd
    
    Path          
    ----          
    C:\Users\kmj04

폴더와 파일 만들기-프로젝트 루트 폴더 생성: mkdir, touch

    PS C:\Users\kmj04> "app","docker","git","logs","data" | ForEach-Object { mkdir "~/dev-workspace/$_" }


    디렉터리: C:\Users\kmj04\dev-workspace


    Mode                 LastWriteTime         Length Name                                                               
    ----                 -------------         ------ ----                                                               
    d-----      2026-11-03  오후 10:09                app                                                                
    d-----      2026-11-03  오후 10:09                docker                                                             
    d-----      2026-11-03  오후 10:09                git                                                                
    d-----      2026-11-03  오후 10:09                logs                                                               
    d-----      2026-11-03  오후 10:09                data                

목록 확인하기: ls, ls -l, ls -a, ls -la, tree

    PS C:\Users\kmj04> ls    
                         
    디렉터리: C:\Users\kmj04

    
    Mode                 LastWriteTime         Length Name                                                               
    ----                 -------------         ------ ----                                                               
    d-----      2026-11-02   오후 9:59                .config                                                            
    d-----      2026-11-03  오전 12:34                .copilot                                                           
    d-----      2026-11-03   오후 8:40                .docker                                                            
    d-----      2026-11-03  오전 12:35                .vscode                                                            
    d-----      2026-11-02  오후 10:02                .vscode-shared                                                     
    d-r---      2026-04-01   오후 5:23                Contacts                                                           
    d-----      2026-11-03  오후 10:09                dev-workspace                                                      
    d-----      2022-12-18   오후 1:23                Documents                                                          
    d-r---      2026-11-03  오전 11:24                Downloads                                                          
    d-r---      2026-04-01   오후 5:23                Favorites                                                          
    d-r---      2026-04-01   오후 5:23                Links                                                              
    d-r---      2026-04-01   오후 5:23                Music                                                              
    dar--l      2026-04-01   오후 5:21                OneDrive                                                           
    d-----      2026-06-23   오후 4:41                Pictures                                                           
    d-r---      2026-04-01   오후 5:23                Saved Games                                                        
    d-r---      2026-04-01   오후 5:23                Searches                                                           
    d-r---      2026-04-01   오후 5:23                Videos                                                             
    d-----      2023-07-06  오후 11:34                vmlogs                                                             
    -a----      2026-11-03   오전 1:12             52 .gitconfig                                                         
    -a----      2023-07-06  오후 11:03             41 inst.ini                                                           
    -a----      2023-07-06  오후 11:03             45 nuuid.ini                                                          
    -a----      2023-07-06  오후 11:03             53 useruid.ini          

권한 정리: chmod 명령어를 사용해야 하는데, powershell 터미널에서는 사용할 수 없어서 chmod 없이 코드를 작성했습니다. 이어지는 권한 변경 과정에서는 사용할 수 없는 원인을 파악하여 chmod 명령어를 사용했습니다. 과제 마지막의 트러블슈팅 경험에서 자세히 기재하겠습니다.

         # 1. 작업 디렉토리로 이동
        >> cd ~\dev-workspace
        >> 
        >> # -----------------------------------------------
        >> # 디렉토리 생성
        >> # -----------------------------------------------
        >> New-Item -ItemType Directory -Force -Path app, docker, git, logs, data
        >> 
        >> # 2. 테스트 파일 생성
        >> New-Item -ItemType File -Force -Path app\index.html
        >> New-Item -ItemType File -Force -Path app\config.yml
        >> New-Item -ItemType File -Force -Path logs\app.log
        >> New-Item -ItemType File -Force -Path app\start.sh
        
        
            디렉터리: C:\Users\kmj04\dev-workspace
        
        
        Mode                 LastWriteTime         Length Name                                                               
        ----                 -------------         ------ ----                                                               
        d-----      2026-11-03  오후 10:09                app                                                                
        d-----      2026-11-03  오후 10:09                docker                                                             
        d-----      2026-11-03  오후 10:09                git                                                                
        d-----      2026-11-03  오후 10:09                logs                                                               
        d-----      2026-11-03  오후 10:09                data                                                               
        
        
            디렉터리: C:\Users\kmj04\dev-workspace\app
        
        
        Mode                 LastWriteTime         Length Name                                                               
        ----                 -------------         ------ ----                                                               
        -a----      2026-11-03  오후 11:09              0 index.html                                                         
        -a----      2026-11-03  오후 11:09              0 config.yml                                                         
        
        
            디렉터리: C:\Users\kmj04\dev-workspace\logs
        
        
        Mode                 LastWriteTime         Length Name                                                               
        ----                 -------------         ------ ----                                                               
        -a----      2026-11-03  오후 11:09              0 app.log                                                            
        
        
            디렉터리: C:\Users\kmj04\dev-workspace\app
        
        
        Mode                 LastWriteTime         Length Name                                                               
        ----                 -------------         ------ ----                                                               
        -a----      2026-11-03  오후 11:09              0 start.sh  
        
        파일 내용 작성 및 실행: cat, bash

절대 경로와 상대 경로는 파일이나 폴더의 주소를 알려주는 방식입니다.

절대 경로: 최상위 루트(C:\ 또는 /)부터 시작해서 전체 이름을 다 적는 방식입니다. 경로가 길지만, 어디서 실행해도 정확히 그 파일을 찾아갑니다.

        예시
        image.png의 절대경로: C:\Users\Student\Downloads\image.png

상대 경로: 현재 내가 있는 위치(Documents, Current Directory)를 기준으로 찾아가는 방식입니다. 경로가 짧고 간결하며, 프로젝트 폴더를 통째로 옮겨도 작동(이식성, Portability)하지만, 내 위치가 바뀌면 경로도 수정해야 합니다.

        예시
        image.png의 상대경로: ../Downloads/image.png

.은 현재 폴더, ..은 상위 폴더입니다. 하위 폴더는 'cd 폴더이름'으로 반드시 폴더 이름을 입력해야 합니다.

파일 권한(r/w/x) 의미: 리눅스나 맥(Unix 계열) 시스템에서 누가 이 파일을 읽고, 쓰고, 실행할 수 있는지 정하는 규칙입니다.

r (read, 읽기, 4): 파일 내용을 보거나 복사할 수 있는 권한입니다.

w (write, 쓰기, 2): 파일 내용을 수정하거나 삭제할 수 있는 권한입니다.

x (execute, 실행, 1): 파일을 프로그램처럼 실행할 수 있는 권한입니다.

권한 없음 = 0

대상의 수에 따라서 자릿수가 달라집니다. 755, 644는 대상이 세 부류이기 때문에 숫자 세 개를 사용합니다.

첫 번째 숫자: 소유자 (Owner) - 파일 주인 (나)

두 번째 숫자: 그룹 (Group) - 같은 팀 멤버

세 번째 숫자: 기타 (Others) - 그 외 모든 사람

755, 644 표기를 해석

755

7(4+2+1: rwx, 소유자가 읽고 쓰고 실행 가능) 5(4+1: r-x, 그룹은 읽고 실행 가능) 5(4+1: r-x, 기타 사용자는 읽고 실행 가능)

644

6(4+2: rw-, 소유자가 읽고 쓰기 가능) 4(4: r--, 그룹은 읽기 가능) 4(4: r--, 기타 사용자는 읽기 가능)

디렉터리 권한 변경

aaa-dir 디렉터리를 생성하고 권한을 777에서 700으로 변경했습니다.

        PS C:\Users\kmj04> mkdir aaa-dir
        
        
            디렉터리: C:\Users\kmj04
        
        
        Mode                 LastWriteTime         Length Name                                                                                                                          
        ----                 -------------         ------ ----                                                                                                                          
        d-----      2026-11-05   오후 3:19                aaa-dir                                                                      
        PS C:\Users\kmj04> docker run -it -v ${PWD}:/home/study ubuntu bash
        root@db185662a4f9:/home/study# ls
         AppData
        'Application Data'
         Contacts
         Cookies
         Documents
         Downloads
         Favorites
         Links
        'Local Settings'
         Music
        'My Documents'
         NTUSER.DAT
         NTUSER.DAT{7f229998-2da2-11f1-8458-e5e6312776f1}.TM.blf
         NTUSER.DAT{7f229998-2da2-11f1-8458-e5e6312776f1}.TMContainer00000000000000000001.regtrans-ms
         NTUSER.DAT{7f229998-2da2-11f1-8458-e5e6312776f1}.TMContainer00000000000000000002.regtrans-ms
         NetHood
         OneDrive
         Pictures
         PrintHood
         Recent
        'Saved Games'
         Searches
         SendTo
         Templates
         Videos
         aaa-dir
         dev-workspace
         inst.ini
         my-web-server
         ntuser.dat.LOG1
         ntuser.dat.LOG2
         ntuser.ini
         nuuid.ini
         useruid.ini
         vmlogs
        ''$'\354\213\234\354\236\221'' '$'\353\251\224\353\211\264'
        root@db185662a4f9:/home/study# ls -ld aaa-dir
        drwxrwxrwx 1 root root 4096 Nov  5 06:19 aaa-dir
        root@db185662a4f9:/home/study# chmod 700 aaa-dir
        root@db185662a4f9:/home/study# ls -ld aaa-dir
        drwx------ 1 root root 4096 Nov  5 06:19 aaa-dir

권한 변경 전/후 비교: 권한 변경 전에는 소유자, 그룹, 기타 사용자 모두 읽기, 쓰기, 실행이 가능했습니다. 권한 변경 후에는 소유자만 읽기, 쓰기, 실행이 가능합니다.

파일 권한 변경

aaa.txt 파일을 생성하고 권한을 644에서 600으로 변경했습니다.

        root@db185662a4f9:/home/study# touch aaa.txt 
        root@db185662a4f9:/home/study# ls -l aaa.txt
        -rw-r--r-- 1 root root 0 Nov  5 07:10 aaa.txt
        root@db185662a4f9:/home/study# chmod 600 aaa.txt
        root@db185662a4f9:/home/study# ls -l aaa.txt
        -rw------- 1 root root 0 Nov  5 07:10 aaa.txt

권한 변경 전/후 비교: 권한 변경 전에는 소유자, 그룹, 기타 사용자 모두 읽기, 쓰기, 실행이 가능했습니다. 권한 변경 후에는 소유자만 읽기, 쓰기, 실행이 가능합니다.

# Docker 운영/검증 로그

Docker 설치 완료 → 버전 확인입니다.

        PS C:\Users\kmj04\dev-workspace> docker --version
        Docker version 29.9.2, build a82e528

Docker 정보 확인입니다.

        PS C:\Users\kmj04\dev-workspace> docker info
        Client:
         Version:    29.9.2
         Context:    desktop-linux
         Debug Mode: false
         Plugins:
          agent: Docker AI Agent Runner (Docker Inc.)
            Version:  v1.152.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-agent.exe
          ai: Docker AI Agent - Ask Gordon (Docker Inc.)
            Version:  v1.33.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-ai.exe
          buildx: Docker Buildx (Docker Inc.)
            Version:  v0.38.1
            Path:     C:\Program Files\Docker\cli-plugins\docker-buildx.exe
          compose: Docker Compose (Docker Inc.)
            Version:  v5.6.1
            Path:     C:\Program Files\Docker\cli-plugins\docker-compose.exe
          debug: Get a shell into any image or container (Docker Inc.)
            Version:  0.49.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-debug.exe
          desktop: Docker Desktop commands (Docker Inc.)
            Version:  4.98.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-desktop.exe
          dhi: CLI for managing Docker Hardened Images (Docker Inc.)
            Version:  v0.0.9
            Path:     C:\Program Files\Docker\cli-plugins\docker-dhi.exe
          extension: Manages Docker extensions (Docker Inc.)
            Version:  v0.2.32
            Path:     C:\Program Files\Docker\cli-plugins\docker-extension.exe
          init: Creates Docker-related starter files for your project (Docker Inc.)
            Version:  v1.4.1
            Path:     C:\Program Files\Docker\cli-plugins\docker-init.exe
          mcp: Docker MCP Plugin (Docker Inc.)
            Version:  v0.44.2
            Path:     C:\Program Files\Docker\cli-plugins\docker-mcp.exe
          model: Docker Model Runner (Docker Inc.)
            Version:  v1.2.9
            Path:     C:\Program Files\Docker\cli-plugins\docker-model.exe
          offload: Docker Offload (Docker Inc.)
            Version:  v0.7.35
            Path:     C:\Program Files\Docker\cli-plugins\docker-offload.exe
          pass: Docker Pass Secrets Manager Plugin (beta) (Docker Inc.)
            Version:  v0.3.2
            Path:     C:\Program Files\Docker\cli-plugins\docker-pass.exe
          sandbox: "docker sandbox" is deprecated, use Docker Sandboxes instead (Docker Inc.)
            Version:  v0.13.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-sandbox.exe
          scout: Docker Scout (Docker Inc.)
            Version:  v1.27.0
            Path:     C:\Program Files\Docker\cli-plugins\docker-scout.exe
        
        Server:
         Containers: 0
          Running: 0
          Paused: 0
          Stopped: 0
         Images: 0
         Server Version: 29.9.2
         Storage Driver: overlayfs
          driver-type: io.containerd.snapshotter.v1
         Logging Driver: local
         Cgroup Driver: cgroupfs
         Cgroup Version: 2
         Plugins:
          Volume: local
          Network: bridge host ipvlan macvlan null overlay
          Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
         CDI spec directories:
          /etc/cdi
          /var/run/cdi
         Discovered Devices:
          cdi: docker.com/gpu=webgpu
         Swarm: inactive
         Runtimes: nvidia runc io.containerd.runc.v2
         Default Runtime: runc
         Init Binary: docker-init
         containerd version: b7a25261e029d68978bbf290df0a62fc819b3c51
         runc version: v1.5.2-0-g29dd3dc2
         init version: de40ad0
         Security Options:
          seccomp
           Profile: builtin
          cgroupns
         Kernel Version: 6.18.54.1-microsoft-standard-WSL2
         Operating System: Docker Desktop
         OSType: linux
         Architecture: x86_64
         CPUs: 16
         Total Memory: 7.568GiB
         Name: docker-desktop
         ID: 4017916d-cdfc-4796-a498-4bf7f28bac64
         Docker Root Dir: /var/lib/docker
         Debug Mode: false
         HTTP Proxy: http.docker.internal:3128
         HTTPS Proxy: http.docker.internal:3128
         No Proxy: hubproxy.docker.internal
         Labels:
          com.docker.desktop.address=npipe://\\.\pipe\docker_cli
         Experimental: false
         Insecure Registries:
          hubproxy.docker.internal:5555
          127.0.0.0/8
          ::1/128
         Live Restore Enabled: false
         Firewall Backend: iptables

<img width="972" height="270" alt="image" src="https://github.com/user-attachments/assets/12196de3-5dfe-4db5-9457-83453c4a7e27" />


Docker 운영 명령 실행 흔적

docker images

컨테이너를 만들기 위한 설계도이자 실행 압축 파일입니다.

IMAGE: 이미지의 이름입니다.

ID: 이미지의 고유 번호입니다.

EXTRA(기타 정보): 추가적인 상태 정보나, 이 이미지가 다른 이미지와 공유하고 있는 데이터가 있는지 등의 부가 정보를 나타냅니다.

i Info →   U  In Use: 도커 이미지들이 어떤 상태인지 보여주는 상태 아이콘입니다.

U(In Use): 이 이미지를 바탕으로 만들어진 컨테이너가 현재 존재한다는 뜻입니다. 나중에 컴퓨터 용량이 부족해져서 안 쓰는 이미지들을 정리해야 할 때 이 표시를 보고 삭제/보존 여부를 판단할 수 있습니다.

i(info): 이미지에 대한 추가적인 정보나 상세 내역을 나타내는 아이콘입니다. 이미지의 태그, 생성일, 레이어 정보 등을 나타내는 일반적인 정보 열(Column)의 머리말입니다.
        
        PS C:\Users\kmj04\dev-workspace> docker images
                                                                                                 i Info →   U  In Use
        IMAGE   ID             DISK USAGE   CONTENT SIZE   EXTRA

docker ps -a

특정 컨테이너가 왜 종료됐는지, 실행 중에 어떤 메시지를 내뱉었는지 확인합니다.
        
        PS C:\Users\kmj04\dev-workspace> docker ps -a
        CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker logs

오류가 생긴 이유: 로그를 볼 컨테이너의 ID나 이름을 docker logs 뒤에 입력하지 않았습니다. 아직 컨테이너 이름 설정에 관한 부분을 잘 모르기 때문입니다.
        
        PS C:\Users\kmj04\dev-workspace> docker logs
        docker: 'docker logs' requires 1 argument

        Usage:  docker logs [OPTIONS] CONTAINER

        Run 'docker logs --help' for more information

docker stats

실행 중인 컨테이너들이 컴퓨터의 자원(CPU, 메모리 등)을 얼마나 쓰고 있는지 실시간 스트리밍으로 보여줍니다.

        CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS


# Dockerfile 기반 웹 서버 컨테이너

docker run hello-world: Docker가 설치되었고, Docker Hub에서 이미지를 가져와 실행할 준비가 끝났습니다.

        PS C:\Users\kmj0403232057> docker run hello-world
        Unable to find image 'hello-world:latest' locally
        latest: Pulling from library/hello-world
        4f55086f7dd0: Pull complete 
        d5e71e642bf5: Download complete 
        Digest: sha256:c567b231f65614688711a75f31518a064258a51d442117a3e771a3a8fdba78ef
        Status: Downloaded newer image for hello-world:latest
        
        Hello from Docker!
        This message shows that your installation appears to be working correctly.
        
        To generate this message, Docker took the following steps:
         1. The Docker client contacted the Docker daemon.
         2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
            (amd64)
         3. The Docker daemon created a new container from that image which runs the
            executable that produces the output you are currently reading.
         4. The Docker daemon streamed that output to the Docker client, which sent it
            to your terminal.
        
        To try something more ambitious, you can run an Ubuntu container with:
         $ docker run -it ubuntu bash
        
        Share images, automate workflows, and more with a free Docker ID:
         https://hub.docker.com/
        
        For more examples and ideas, visit:
         https://docs.docker.com/get-started/

ubuntu 컨테이너 실행, 내부 진입

        PS C:\test\집> docker run -it --name study-ubuntu ubuntu bash
        root@b22a5bf54131:/# 

ls: 파일 목록을 확인하는 명령어입니다.

        root@b22a5bf54131:/# ls
        bin   dev  home  lib64  mnt  proc  run   srv  tmp  var
        boot  etc  lib   media  opt  root  sbin  sys  usr

echo: 텍스트 출력 명령어입니다.

        root@b22a5bf54131:/# echo "a"           
        a

docker 명령어는 원래 내 컴퓨터 터미널에서 실행해야 하기 때문에 exit 명령어를 입력해서 나갑니다.

docker ps -a: 컴퓨터에 존재하는 모든 컨테이너의 리스트입니다.

        PS C:\Users\kmj0403232057> docker ps -a
        CONTAINER ID   IMAGE         COMMAND                   CREATED          STATUS                     PORTS                                     NAMES
        e33e451f4c3a   hello-world   "/hello"                  8 minutes ago    Exited (0) 8 minutes ago                                             goofy_carson

폴더 만들기: 바탕화면에 my-web-server 폴더 생성 후 mkdir 명령어 입력

        PS C:\Users\kmj0403232057\my-web-server> mkdir my-web-server
        
        
            디렉터리: C:\Users\kmj0403232057\my-web-server
        
        
        Mode                 LastWriteTime         Length Name                                                                   
        ----                 -------------         ------ ----                                                                   
        d-----      2026-11-04  오후 12:06                my-web-server         

폴더 안으로 들어가기

        PS C:\Users\kmj0403232057\my-web-server> cd my-web-server
        PS C:\Users\kmj0403232057\my-web-server\my-web-server> 
        
index.html 만들기

        PS C:\Users\kmj0403232057\my-web-server> @'
        >> <!DOCTYPE html>
        >> <html>
        >> <body>
        >>     <h1>hello-world</h1>                     
        >> </body>                                                 
        >> </html>
        >> '@ | Out-File -FilePath index.html -Encoding utf8

Dockerfile 만들기

        PS C:\Users\kmj0403232057\my-web-server> @'         
        >> FROM nginx:alpine
        >> COPY index.html /usr/share/nginx/html/index.html
        >> '@ | Out-File -FilePath Dockerfile -Encoding ascii

Dockerfile과 index.html이 잘 만들어졌는지 확인

        PS C:\Users\kmj0403232057\my-web-server> cat index.html
        <!DOCTYPE html>
        <html>
        <body>
        <h1>hello-world</h1>
        </body>
        </html>
        PS C:\Users\kmj0403232057\my-web-server> cat dockerfile
        FROM nginx:alpine
        COPY index.html /usr/share/nginx/html/index.html

my-web-page 이미지 만들기

'-t': 이미지의 이름을 지어줍니다.

'.': 현재 디렉토리(지금 내가 있는 이 폴더)에서 Dockerfile을 찾아보라는 의미입니다.

        PS C:\Users\kmj0403232057\my-web-server> docker build -t my-web-page .
        [+] Building 1.7s (7/7) FINISHED                                                                     docker:desktop-linux
         => [internal] load build definition from Dockerfile                                                                 0.0s
         => => transferring dockerfile: 105B                                                                                 0.0s
         => [internal] load metadata for docker.io/library/nginx:alpine                                                      1.3s
         => [internal] load .dockerignore                                                                                    0.0s
         => => transferring context: 2B                                                                                      0.0s
         => [internal] load build context                                                                                    0.0s
         => => transferring context: 112B                                                                                    0.0s
         => CACHED [1/2] FROM docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698  0.0s
         => => resolve docker.io/library/nginx:alpine@sha256:785835ea65db4bba6f021acc0f3be91b0fef76a53fe41f8588c6698d2aed06  0.0s
         => [2/2] COPY index.html /usr/share/nginx/html/index.html                                                           0.0s
         => exporting to image                                                                                               0.2s
         => => exporting layers                                                                                              0.1s
         => => exporting manifest sha256:ace7d2d9ad1323acd1a2e6c81b4e4bcfe5090ee7a5b72fdde5245bd0a1fb7d59                    0.0s
         => => exporting config sha256:520c3d8e3eb0c93df1b593f62a9d6a37b6579caa09fa7af43e118a9332edb0bb                      0.0s
         => => exporting attestation manifest sha256:7407a1b80bd520c689ac85465e0420666bfe824c3f59e15fc400268dd09e5e77        0.0s
         => => exporting manifest list sha256:bf179243270e9ec89b31fbcb8758585301225a93979721d4d8caff03360f2f48               0.0s
         => => naming to docker.io/library/my-web-page:latest                                                                0.0s
         => => unpacking to docker.io/library/my-web-page:latest                                                             0.0s

컨테이너 이름을 E1-1로 정하고 컨테이너 실행하기

        PS C:\Users\kmj0403232057\my-web-server> docker run -d -p 8080:80 --name E1-1 my-web-page
        af50cac65f3e47460d500114bdead5be648a369586bba9768b46953306fbe1c3

# 포트 매핑 접속 증거

웹 서버 실행 확인

        PS C:\Users\kmj0403232057\my-web-server> docker ps
        CONTAINER ID   IMAGE         COMMAND                   CREATED         STATUS         PORTS                                     NAMES
        af50cac65f3e   my-web-page   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   E1-1

<img width="1448" height="476" alt="image" src="https://github.com/user-attachments/assets/39f39582-a204-4952-893b-6f25a5e147cb" />

웹 서버 링크 http://localhost:8080/

<img width="621" height="359" alt="image" src="https://github.com/user-attachments/assets/df662a3f-98b8-4157-93e1-fddc5b36364b" />

포트 매핑이 필요한 이유: 내 호스트 포트와 컨테이너 포트를 연결하면 외부 사용자가 내 포트로 컨테이너에 접근할 수 있습니다. 

# 바인드 마운트 반영 + 볼륨 영속성 증거

바인드 마운트 반영

        PS C:\Users\kmj0403232057\my-web-server> docker run -d -p 8081:80 -v C:\Users\kmj0403232057\my-web-server:/usr/share/nginx/html --name E1-2 my-web-page                                                                                        
        85563de22774ed99cc64b9f8b2bea75f6fed5cb92f469259bb80adb441564d39

<img width="1420" height="525" alt="image" src="https://github.com/user-attachments/assets/54c0f1fb-95f9-4967-a47f-5239907be1fa" />

실행 명령: docker run -d -p [포트번호] -v

도커 옵션

-p (Publish): 포트 매핑 - 내 컴퓨터의 문(포트)와 컨테이너의 문을 연결합니다.

-d (Detached): 백그라운드 실행 - 컨테이너를 백그라운드에서 실행합니다. 컨테이너가 실행되는 동안 터미널 창에 다른 명령어를 입력하기 위해 필요한 기능입니다.  웹 서버처럼 계속 켜져 있어야 하는 프로그램에 필수입니다.

-v (Volume): 바인드 마운트/볼륨 - 내 컴퓨터의 폴더와 컨테이너 안의 폴더를 실시간으로 동기화합니다. 코드 수정 시 컨테이너에 즉시 반영되도록 하거나 영속성을 위해 사용합니다.

--name: 컨테이너 이름 설정 - 이름이 없으면 무작위로 이름이 설정됩니다.

--rm: 컨테이너가 종료되면 자동으로 삭제합니다.

호스트 변경 전/후 비교: docker를 사용하면 컴퓨터를 옮겨서 호스트가 변경되어도 docker run을 입력하면 동일한 컨테이너로 간편하게 환경을 맞출 수 있습니다.

볼륨 영속성 증거

E1-2 index.html 파일 불러오기 → 내용 수정 → 저장

        PS C:\Users\kmj0403232057\my-web-server> code index.html
        
        <!DOCTYPE html>
        <html>
        <head>
        <title>영속성 테스트</title>
        </head>
        <body>
        <h1>바인드 마운트 연결 성공!</h1>
        <p>현재 상태: 컨테이너 E1-2와 내 폴더가 연결되어 있습니다.</p>
        </body>
        </html>

<img width="587" height="288" alt="image" src="https://github.com/user-attachments/assets/3c445cfa-2cad-466f-9db1-b64359738a67" />

E1-2 삭제

-f: 실행 중인 컨테이너를 강제로(force) 끄고 삭제 → http://localhost:8081 사라짐

        PS C:\Users\kmj04\my-web-server> docker rm -f E1-2
        E1-2

새로운 컨테이너 E1-3 만들었을 때 index.html 파일이 그대로 남아있는지 확인

        PS C:\Users\kmj04\my-web-server> docker run -d -p 8082:80 --name E1-3 -v C:\Users\kmj04\my-web-server:/usr/share/nginx/html my-web-page
        3bb373abc1e6334e272c02ec84b53205226b2529cd8c4bf4c1844c9a523f6537

<img width="1212" height="187" alt="image" src="https://github.com/user-attachments/assets/60347c39-a496-4cf5-8b5b-cd9b9f6ab55d" />
웹 서버 링크 http://localhost:8082/
<img width="628" height="327" alt="image" src="https://github.com/user-attachments/assets/558c0cc8-244a-40dc-bfdd-e821913daafe" />

컨테이너 삭제 전/후 비교: 컨테이너는 사라져도 바인드 마운트(-v)로 연결한 데이터는 사라지지 않았습니다. 바인드 마운트나 볼륨으로 데이터를 호스트에 안전하게 보관했기 때문입니다.

# Git 설정 및 GitHub/VSCode 연동 증거

Git 설정

        PS C:\Users\kmj04\my-web-server> git config --global user.name "byabii0"
        PS C:\Users\kmj04\my-web-server> git config --global user.email "kmj040323@gmail.com"
        PS C:\Users\kmj04\my-web-server> git config --list
        diff.astextplain.textconv=astextplain
        filter.lfs.clean=git-lfs clean -- %f
        filter.lfs.smudge=git-lfs smudge -- %f
        filter.lfs.process=git-lfs filter-process
        filter.lfs.required=true
        http.sslbackend=schannel
        core.autocrlf=true
        core.fscache=true
        core.symlinks=false
        pull.rebase=false
        credential.helper=manager
        credential.https://dev.azure.com.usehttppath=true
        init.defaultbranch=master
        user.name=byabii0
        user.email=kmj040323@gmail.com

GitHub/VSCode 연동 증거

로컬 저장소 만들기 및 커밋

        PS C:\Users\kmj04\my-web-server> git init
        Initialized empty Git repository in C:/Users/kmj04/my-web-server/.git/
        PS C:\Users\kmj04\my-web-server> git add .
        warning: in the working copy of 'Dockerfile', LF will be replaced by CRLF the next time Git touches it
        warning: in the working copy of 'index.html', LF will be replaced by CRLF the next time Git touches it
        PS C:\Users\kmj04\my-web-server> git commit -m "First Commit"
        [master (root-commit) 1768a40] First Commit
         2 files changed, 12 insertions(+)
         create mode 100644 Dockerfile
         create mode 100644 index.html

<img width="880" height="381" alt="image" src="https://github.com/user-attachments/assets/377cf88f-6cd1-4dd3-9214-9607dab47d35" />

GitHub 원격 저장소 연결 및 Push

        PS C:\Users\kmj04\my-web-server> git remote add origin https://github.com/byabii0/E1-1.git
        PS C:\Users\kmj04\my-web-server> git branch -M main
        PS C:\Users\kmj04\my-web-server> git push -u origin main
        Enumerating objects: 7, done.
        Counting objects: 100% (7/7), done.
        Delta compression using up to 16 threads
        Compressing objects: 100% (6/6), done.
        Writing objects: 100% (6/6), 836 bytes | 167.00 KiB/s, done.
        Total 6 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
        To https://github.com/byabii0/E1-1.git
           6b144a2..b50435c  main -> main
        branch 'main' set up to track 'origin/main'.



