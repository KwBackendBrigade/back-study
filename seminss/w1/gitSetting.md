> ### Server -> Local

외부 Repository Fork
1. **`git clone [외부 repository URL]`** : 프로젝트 clone
   2. url 복사 명령어 : shift +fn +insert
1. **`git remote -v`** : 현재 연결된 remote repository 확인
2. **`git remote set-url origin [fork된 내 repository URL]`** : 기존 원격 저장소 URL을 변경(내걸루) + 약칭은 origin으로 하겠습니다~
3. **`git remote -v`** : remote repository 잘 수정됐는지 확인
4. **`git add .`**
5. **`git commit -m “commit message”`**
6. **`git push origin main`** : 내 브랜치 생성하기 전에 main branch로 첫 커밋
7. **`git checkout -b [내 branch 이름]`** : 브랜치 생성
8. 코드 작성
9. **`git push origin [내 브랜치]`**

Fork 하는 경우가 아니라, 내가 repository를 생성 했을 때도 유사하다.

<br/>

> ### Local -> Server

만약 local 프로젝트나 디렉토리를 Git 저장소로 만들고 싶을 때는
1. `cd [절대주소 or 상대주소]` : Local 저장소 위치로 이동
2. `git init` : git 저장소 생성
3. github에서 remote repository 만들기
4. `git remote add origin [github URL]` : 원격 저장소와 로컬 저장소 연결
5. `add`, `commit`, `push` + 나머진 사실 다 똑같음

<br/>

---


git 명령어 정리 : https://codingtrainee.tistory.com/144
