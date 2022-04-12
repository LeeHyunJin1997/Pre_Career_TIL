- `git branch` : 브랜치 목록 확인

- `git branch branch_name` : branch_name이라는 새로운 브랜치 생성

- `git branch -d branch_name` : branch_name에 해당하는 브랜치 삭제
  - 병합된 브랜치만 삭제
- `git branch -D branch_name` : 강제 삭제

- `git switch branch_name` : 다른 브랜치로 이동

- `git switch -c branch_name` : 브랜치를 생성과 동시에 이동





- `git merge branch_name` : 병합
  - 병합하기 전에 메인 브랜치로 이동해야함



## 1. fast-forward

- master branch에 변화가 없는 상황에서, 다른 브랜치로 나아감



## 2. 3-way merge



## 3. merge conflict

- 두 브랜치에서 같은 파일의 같은 부분을 수정했을 경우
- git이 해당 부분을 자동으로 merge하지 못하고 충돌

