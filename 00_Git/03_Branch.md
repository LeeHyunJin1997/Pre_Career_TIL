# Branch

> 나뭇가지처럼 여러 갈래로 작업 공간을 나누어주는 Git의 도구
>
> - 원래 코드에 영향을 주지 않고 작업할 수 있다.
> - 하나의 작업은 하나의 브랜치로 나누어 작업, 동시에 체계적으로 개발 가능
> - Git의 브랜치는 매우 가벼워 순식간에 브랜치를 새로 만들고 브랜치 사이를 이동 가능



# Branch Command

- `git branch` : 브랜치 목록 확인
- `git branch -r` : 원격 저장소의 브랜치 목록 확인
- `git branch branch_name` : branch_name이라는 새로운 브랜치 생성
- `git branch -d branch_name` : branch_name에 해당하는 브랜치 삭제
  - 병합된 브랜치만 삭제
- `git branch -D branch_name` : 병합되지 않은 브랜치도 강제 삭제 
- `git switch branch_name` : 다른 브랜치로 `HEAD`를 이동
  - `HEAD` : 현재 브랜치를 가리키는 포인터
- `git switch -c branch_name` : 브랜치를 생성과 동시에 이동

- `git merge branch_name` : 병합
  - 병합하기 전에 메인 브랜치로 이동해야함



# Switch 주의사항

> Git의 브랜치는 관리하는 파일 트리에 한해서만, 독립적인 작업 공간을 갖기 때문에,
>
> feature 브랜치에서 파일을 생성하고 git add 하지 않은 상태에서 master 브랜치로 이동한다면
>
> master 브랜치에도 같은 파일이 생성
>
> 따라서, 반드시 switch하기 전에 모든 파일이 버전 관리되고 있는지 확인!





---



# Branch Merge

>  `git merge branch_name`  
>
> 작업이 완료된 각 브랜치를 병합하는 것
>
> 병합하기 전, 메인 브랜치로 switch 해야 한다
>
> 병합한 후, 필요없어진 브랜치는 삭제



### Merge의 종류

#### 1. fast-forward

>  master branch에 변화가 없는 상황에서, 다른 브랜치로 나아가는 병합



#### 2. 3-way merge

> 두 브랜치의 커밋과 공통 조상 하나를 사용하여 병합
>
> 두 브랜치에서 다른 파일 혹은 같은 파일의 다른 부분을 수정했을 때 가능



#### 3. merge conflict

> 두 브랜치에서 같은 파일의 같은 부분을 수정했을 경우
>
> Git이 해당 부분을 자동으로 merge하지 못하고 충돌
>
> 사용자가 직접 내용을 선택해서 해결해야함

