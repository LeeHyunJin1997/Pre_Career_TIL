# Git

- 분산 버전 관리 시스템 (DVCS)
- 코드의 히스토리(버전)을 관리
- 변경사항만을 저장(모든 버전을 합쳐야 한 파일이 나옴)



# Command-Line Interface (CLI)

- 명령 프롬프트와 Power shell

- 명령 프롬프트는 윈도우가 기본 제공하는 shell. 단, Unix/Linux 명령어를 사용할 수 없음.

- Power shell에서는 Unix/Linux 명령어가 일부 동작

  ## Unix/Linux 명령어

  - `ls` : 현재 위치의 폴더, 파일 목록 보기
  - `cd <path>` : 현재 위치 path로 이동하기
  - `cd ..` : 상위 폴더로 이동하기
    - `..`은 일반적으로 상위폴더를 의미
  - `mkdir <name>` : name이라는 폴더 만들기
  - `touch <name>` : name이라는 파일 만들기
  - `rm <name>` : name이라는 파일 지우기
  - `rm -r <name>` : name이라는 폴더 지우기
    - `-r` : recursive. 더 안쪽 파일까지 한번 동작
    - `-rf` : 보호 받는 파일도 삭제
  - `~` : home dir. 계정의 기본 위치
  - `code .` : 현재 위치에서 vscode 실행
    - `.`은 일반적으로 현재 위치를 의미
  - `git init` : 현재 위치를 Repository로 지정
    - Repository : Git으로 버전 관리를 할 저장소
    - Repository로 지정하면 .git 폴더가 생성되며 분산 파일이 저장됨
    - 지정된 폴더의 하위 폴더는 자동으로 관리의 대상이 됨



# Commit

- 커밋은 특정 버전을 저장하는 것

- 커밋 동작 유형

  - Working Directory : 작업 중인 실제 디렉토리

  - Staging Area : 커밋으로 남기고 싶은 특정 버전으로 관리하고 싶은 파일이 임시로 남는 곳

  - Repository : 커밋이 최종적으로 저장되는 곳 

- 새로 생성된 파일은 Git이 추적하지 않으며 Working Directory에 존재 (untracked files)

- `git add`를 이용해 Staging Area로 파일을 이동 (staged)

  - `git add .` : 추적되지 않은 모든 파일과 추적하고 있는 파일 중 수정된 파일을 모두 Staging Area로 이동

- `git commit`을 써서 커밋

  - `-m "explain"` 을 붙여 커밋 메시지를 작성할 수 있음 (자세하게 작성)

- `git status` : Git이 추적하고 있는 현상환을 확인

- `git log` : 커밋된 파일의 고유번호, 커밋메시지를 확인

- `git diff <commit1> <commit2>` :  커밋된 파일을 비교. commit1을 기준으로 변화를 보여줌

- `git config user.name "name"`,`git config user.email "email" ` : 해당 폴더에서 작업하는 사용자 정보를 입력해야 커밋 가능



# GitHub 

- Git을 이용해 버전 관리된 데이터를 보관하는 저장소
- 종류
  - GitLab
  - GitHub (마이크로소프트)
  - Bitbucket
- `git clone <url>` : 해당 url의 Repository를 현재 위치로 복사해옴

  - 복사한 repo는 이미 `git init`된 것과 같음
  - repo를 통째로 가져오는 것이기 때문에, 작업시 최초 1회 실행함 
- `git pull` : commit 단위로 local repo로 가져옴
- `git push` : commit 단위로 remote repo로 보냄
- `git remote add origin <url>` : remote를 origin이라는 이름으로 연동

  - `origin` : 통상적으로  remote repo를 가리킴
  - `git push -u origin master` :  origin의 master로 보냄
    - `-u` : set upstream. 최초 1회, orgin의 master임을 지정하기 위함



# README.md

- 커밋에 대한 설명
- 과제 및 학습용에는 다음을 포함
  - 무엇을 배웠는가
  - 어떤 문제가 있었고, 어떻게 해결했는가 
  - 추가적으로 학습한 내용은 무엇인가




# Conflict

- 최신 버전으로 pull하지 않고 수정해 push한 경우, 충돌에러(Conflict) 발생



# Vi

- `vi <file.name>` : 해당 파일에 접근

- `i` : INSERT. 내용 작성 가능

- `:`  : 명령어 입력

- `:wq` : 저장하고 종료





