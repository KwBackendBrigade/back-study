깃허브 사용법
==========

### 1. 초기 설정    
    git config --global user.name "user_name"  
    git config --global user.email your_email    
>#### 초기 설정 완료 및 폴더와 파일 생성
    git init
- - -
### 2. *Git*에서 버전이 만들어지는 과정

* 작업 디렉토리
* 스테이지 - *다음 버전이 될 후보가 올라가는 공간*
* 저장소 - *Commit 내용들이 쌓이는 공간*

>#### 2.1 작업 디렉토리 > 스테이지
    git add filename

>#### 2.2 스테이지 > 저장소
    git commit -m "Message"
- - - 
### 3. 파일 관리 Git 명령어


>#### 어떤 파일이 Modified 되었는지
    git status

  * *Stage에서 Commit할 시 unmodified 된다 !*

>#### 커밋에 대한 조회
    git log --oneline : 단순조회
    git log --patch : 각각의 커밋의 변경내역을 상세히 표시
    git log --graph : 커밋을 그래프 형태로 출력

>#### 커밋에 대한 별칭 추가
    git tag [tag명][commit명]
*  *git tag -l : 태그 조회하기*
*  *git tag -d [tag명] : 태그 삭제하기*

### 4. 브랜치(Branch)
 * 버전을 **여러 흐름으로 나누어서 관리** 하는 방법
    * 각자 기능을 맡아서 따로 개발하는 경우
    * 새로운 요구사항을 반영한 다양한 버전
- - -
>#### 4.1 브랜치 명령어 
    
    git branch : 현재 작업중인 branch 확인하기
    git branch [branch명] : 브랜치 나누기
####
    git checkout [branch명] : 특정 브랜치로 전환하기
    git checkout -b [branch명] : branch 만들면서 바로 checkout 하기
####
    git branch -d [branch명] : 브랜치 삭제

>#### 4.2 브랜치 병합하기
    git merge [병합할 branch]
* *A branch를 master branch에 병합하고 싶을 떄 : master branch로 checkout 후 git merge A* 
- - -
### 5. Github를 활용한 협업

>#### 5.1 원격 저장소 복제해오기
    git clone [원격저장소경로]
* *github에 있는 환경을 나의 Local로 가져오는 것 !*
- - -
>#### 5.2 원격 저장소 관련 명령어
- 원격 저장소 이름 origin을 추가함
###
    git remote add origin [원격저장소경로]
- 원격 저장소 목록 조회
###
    git remote -v 
- 이름을 origin 에서 change로 변경
###
    git remote rename origin changed
- - -
>#### 5.2 로컬과 원격 저장소 동기화
    git push [원격저장소] [브랜치이름]
>#### 5.3 원격과 로컬 저장소를 동기화
    git pull [원격저장소] [브랜치이름]
###
* *pull시 자동으로 Merge가 되니 Merge를 원치 않을 때는 fetch 명령어 사용 !*
* ___git pull = git fetch + git merge___
- - -
### ~~마크다운 언어가 익숙하지 않아 디자인이 미흡함~~