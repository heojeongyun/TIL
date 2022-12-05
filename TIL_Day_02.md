# TIL Day 02

>2022년 12월 2일 금요일

## 1) Github README
---
깃허브를 포트폴리오화 할 때 대문이 되는 프로필을 만들 수 있다.

### *대문 README를 만들 수 있는 조건*
- 깃허브 사용자 이름과 일치하는 이름으로 repository를 만들 때
- 공개 repository일 때
- README.md라는 파일이 있고 파일에 모든 콘텐츠가 포함되어 있을 때

## 2) git clone, git pull
---
### *git clone*
- 원격 저장소의 커밋 내용을 모두 가져와서 로컬 저장소를 생성하는 명령어
- ```git clone <원격 저장소 주소>```의 형태로 작성
- git clone을 통해 생성된 로컬 저장소는 ```git init```과 ```git remote add```가 이미 수행되어 있음

### *git pull*
- 원격 저장소의 변경 사항을 가져와서 로컬 저장소를 업데이트 하는 명령어
- ```git pull <저장소이름> <브랜치이름>```의 형태로 작성
- **git clone은 처음 한 번만 실행**

## 3) .gitignore
---
>특정 파일 혹은 폴더에 대해 Git이 버전 관리를 하지 못하도록 지정하는 것

### *.gitignore에 작성하는 목록*
- 민감한 개인 정보가 담긴 파일
- OS에서 활용되는 파일
- IDE 혹은 Text editor(vs code) 등에서 활용되는 파일
- 개발 언어 혹은 프레임워크에서 사용되는 파일

### *.gitignore 작성 시 주의 사항*
- 반드시 이름을 ```.gitignore```로 작성
- ```.gitignore``` 파일은 ```.git``` 폴더와 동일한 위치에 생성
- **제외하고 싶은 파일은 반드시 ```git add``` 전에 ```.gitignore```에 작성**

### *.gitignore 쉽게 작성하기*

#### 1. 웹사이트
[gitignore 링크](https://www.toptal.com/developers/gitignore/)

#### 2. gitignore 저장소
[gitignore 저장소](https://github.com/github/gitignore)


### *gitignore 패턴 예시*

```bash
# .gitignore

# 확장자가 txt인 파일 무시
*.txt

# 현재 확장자가 txt인 파일이 무시되지만, 느낌표를 사용하여 test.txt는 무시하지 않음
!test.txt

# 현재 디렉터리에 있는 TODO 파일은 무시하고, folder/TODO 처럼 하위 디렉터리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉터리에 있는 모든 파일은 무시
build/

# folder/notes.txt 파일은 무시하고 folder/child/arch.txt 파일은 무시하지 않음
folder/*.txt

# folder 디렉터리 아래의 모든 .pdf 파일을 무시
folder/**/*.pdf
```

## 4. Branch
---
>나뭇가지처럼 여러 갈래로 작업 공간을 나누어 독립적으로 작업할 수 있도록 도와주는 도구

- 장점
 1. 브랜치는 독립 공간을 형성하기 때문에 원본(master)에 대해 안전함
 2. 하나의 작업은 하나의 브랜치로 나누어 진행되므로 체계적인 개발이 가능함
 3. 깃은 특히 브랜치를 빠르고 용량 적게 만들 수 있음
  
### *git Branch*
>브랜치 ```조회, 생성, 삭제 등``` 브랜치와 관련된 Git 명령어

```bash
# 브랜치 목록 확인
$ git branch

# 원격 저장소의 브랜치 목록 확인
$ git branch -r

# 새로운 브랜치 생성
$ git branch <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성
$ git branch <브랜치 이름> <커밋 ID>

# 특정 브랜치 삭제
$ git branch -d <브랜치 이름> # 병합된 브랜치만 삭제 가능
$ git branch -D <브랜치 이름> # (주의) 강제 삭제 (병합되지 않은 브랜치도 삭제 가능)
```
### *git switch*
>현재 브랜치에서 다른 브랜치로 ```HEAD```를 이동시키는 명령어

```bash
# 다른 브랜치로 이동
$ git switch <다른 브랜치 이름>

# 브랜치를 새로 생성과 동시에 이동
$ git switch -c <브랜치 이름>

# 특정 커밋 기준으로 브랜치 생성과 동시에 이동
$ git switch -c <브랜치 이름> <커밋 ID>
```
- 브랜치를 이동한다는 건 HEAD가 해당 브랜치를 가리킨다는 것을 의미함
- HEAD는 해당 브랜치의 최신 커밋을 가리키게 됨

## 5) Branch-merge
---
### *git merge*
- 분기된 브랜치들을 하나로 합치는 명령어
- ```git merge <합칠 브랜치 이름>```의 형태로 사용
- Merge하기 전에 일단 다른 브랜치를 합칠, 즉 메인 스위치로 switch 해야 한다.

```bash
# 1. 현재 branch1과 branch2가 있고, HEAD가 가리키는 곳은 branch1 입니다.
$ git branch
* branch1
  branch2

# 2. branch2를 branch1에 합치려면?
$ git merge branch2

# 3. branch1을 branch2에 합치려면?
$ git switch branch2
$ git merge branch1
```

### *Merge의 세 종류*
1. Fast-Foward
   - 브랜치를 병합할 때 마치 빨리감기처럼 브랜치가 가리키는 커밋을 앞으로 이동시키는 것
   - 따로 merge과정 없이 브랜치의 포인터가 이동하는 것

2. 3-Way Merge
   - 브랜치를 병합할 때 각 브랜치의 커밋 두 개와 공통 조상 하나를 사용하여 병합하는 것
   - 두 브랜치에서 다른 파일 혹은 같은 파일의 다른 부분을 수정했을 때 가능
   - 공통 조상과 각자가 가리키는 커밋을 비교하며 진행, 두 브랜치가 병합되면서 Merge Commit이 발생함

3. Merge Conflict
   - 병합하는 두 브랜치에서 같은 파일의 같은 부분을 수정한 경우, Git이 어느 브랜치의 내용으로 작성해야 하는지 판단하지 못해서 발생
   - 결국은 사용자가 직접 내용을 선택해서 해결
   - 같은 파일의 같은 부분을 수정, 병합할 때 발생
 - 병합이 완료된 브랜치 삭제하기
  ```bash
  $ git branch -d <브랜치명>
  ```
  ## 6. Git Workflow 개념
  ---
  ### *1. 원격 저장소 소유권이 있는 경우*
  - 원격 저장소가 자신의 소유이거나 collaborator로 등록되어 있는 경우
  - master에 직접 개발하는 것이 아니라 기능별로 브랜치를 따로 만들어서 개발
  - ```Pull Request```를 같이 사용하여 팀원 간 변경 내용에 대한 소통을 진행함

>Pull Request= 브랜치를 master에 반영해달라는 요청을 보내는 것

### *2. 원격 저장소 소유권이 없는 경우*
- 오픈 소스 프로젝트처럼 자신의 소유가 아닌 원격 저장소인 경우
- 원본 원격 저장소를 그대로 내 원격 저장소에 복제 (이 행위를 ```fork```라고 함)
- 기능 완성 후 Push는 복제한 내 원격 저장소에 진행!
- 이후 ```Pull Request```를 통해 원본 원격 저장소에 반영될 수 있도록 요청
