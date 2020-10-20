# 📚 Git 용어정리

## 📂 Repository
: 파일이나 폴더를 저장하는 저장소를 의미하며, 저장소는 히스토리, 태그, 소스의 가지치기 혹은 branch에 따라 버전을 관리하며 변경한 모든 히스토리를 확인할 수 있음  
- 원격 저장소(Remote Repository) : 파일이 원격 저장소 전용 서버에서 관리되며 여러 사람이 함께 공유하기 위한 저장소(GitHub 등)
- 로컬 저장소(Local Repository) : 내 PC에 파일이 저장되는 개인 전용 저장소를 의미

## 📩 Commit
- 파일 및 폴더의 추가/변경 사항을 저장소에 기록
- 커밋은 시간순으로 저장되기 때문에 최근 커밋부터 거슬러 올라가면 과거 변경 이력과 내용을 알 수 있음
- 각 커밋에는 영문/숫자로 이루어진 40자리 고유 이름이 붙어 각 커밋을 식별 가능(commit d7d565b4bb08cb9b432192c8ecee968d9b12d641)
- 커밋은 이력을 남기는 중요한 작업이기 때문에 커밋 메세지를 필수로 입력해야함

## 📖 Git Area
1. Working Directory(작업영역)
    - 실제 프로젝트 디렉토리, git 이력과 관련된 정보가 저장되어있는 모든 영역을 의미(.git 제외)
    - 실제 코드 수정과 추가 등 변경이 이루어지는 영역
1. Index(= Staging Area)
    - Working Directory에서 Repository(저장소)로 정보가 저장되기 전 준비 영역
    - 파일 상태로 기록, 스테이징 한다고도 표현
    - git add 명령어로 Working Directory에서 Index 영역으로 정보가 저장
1. Repository(저장소)
    - 파일이나 폴더를 변경 이력별로 저장해 두는 곳
    - .git디렉토리 내에 존재
    - git commit 명령어로 Index 영역에서 Repository로 정보가 저장
4. Stash
    - 일반적인 WorkingDirectory > Index > Repository로 이루어지는 영역과는 별개의 임시영역(임시적으로 저장해놓고 나중에 꺼내올 수 있음)

## 🧬 Status
- untracked : 깃에 의해 주적되고 있지 않은 상태(git add 이전 상태)
- tracked
    - staged : 파일이 수정되고 나서 staging area에 올라오는 상태
    - unmodified : 현재 파일 내용이 최신 커밋과 같을 때(커밋하고 난 직후의 파일)
    - modified : 최근 커밋과 비교해서 바뀐 내용이 있는 상태

## 🎸 ETC
- HEAD : 현재 작업중인 브랜치를 의미
- Branch : 가지 또는 분기점을 의미하며, 여러 개발자들이 각자 독립적인 영역(저장소)안에서 소스코드를 수정할 수 있게 함
- Merge : 다른 Branch의 내용을 현재 Branch로 가져와 합치는 작업을 의미
- Tag : 커밋을 참조하기 쉽도록 알기 쉬운 이름을 붙이는 것
    - 일반태그 : 이름만 붙일 수 있음
    - 주석태그 : 이름과 태그에 대한 설명, 서명, 만든 사람 이름, 이메일과 만든 날짜 정보도 포함할 수 있음

## 💻 Git 자주쓰이는 명령어
- **git init** : 현 디렉토리를 working directory로 설정하고 그 안에 레포지토리(.git) 생성
- **git config user.name "username"** : 현재 사용자 아이디를 ""안에 이름으로 설정
- **git config user.email "email"** : 현재 사용자 이메일을 ""안에 이름으로 설정
- **git add [파일명]** : 바뀐 것이 있는 해당 파일을 staging area(Index)에 올림(폴더명이면 내부의 모든 파일 해당)
- **git add .** : workig directory 내의 바뀐 것이 있는 모든 파일을 staging area에 올림(= git add *)
- **git reset [파일명]** : staging area에 올렸던 파일 취소
- **git status** : 현재 프로젝트 관련 내용들 출력(파일의 현재 상태 등)
- **git commit -m "커밋메시지"** : 현재 staging area에 있는 것들을 커밋으로 남기기
- **git help [커맨드 이름]** : git 커맨드의 공식 매뉴얼 출력
- **git push -u origin master** : 로컬 레파지토리의 내용을 처음으로 원격 레파지토리에 올릴 때 사용
- **git push** : 로컬 레파지토리의 내용을 원격 레파지토리에 보내기
- **git pull** : 원격 레파지토리의 내용을 로컬 레파지토리로 가져오기
- **git clone [깃허브 주소]** : github에 있는 프로젝트를 본인 컴퓨터로 가져오기
- **git log** : 커밋 히스토리
- **git log --pretty=oneline** : 커밋 하나당 한 줄로 히스토리 출력
- **git show [커밋/태그 아이디]** : 특정 커밋에서 어떤 변경 사항이 있었는지 확인
- **git commit --amend** : 최신 커밋을 수정하여 새로운 커밋으로 만듦
- **git comfig alias.[이름] [커맨드]** : 해당 커맨드를 git[이름] 만으로 실행할 수 있도록 설정
- **git diff [커밋 A 아이디] [커밋 B 아이디]** : 두 커밋 간 차이 비교
- **git tag [태그이름] [커밋아이디]** : 특정 커밋에 태그를 붙임
- **git tag** : 태그 조회
- **git reset [옵션] [커밋아이디]**
    - **--soft** : HEAD가 특정 커밋을 가리킴
    - **--mixed(default)** : staging area도 특정 커밋처럼 리셋
    - **--hard** : working directory까지 특정 커밋처럼 리셋
    - 커밋 아이디 대신 HEAD^, HEAD~3 등의 방식도 가능
- **git branch [브랜치 이름]** : 새로운 브랜치 생성
- **git checkout -b [브랜치 이름]** : 새로운 브랜치 생성 후 바로 이동
- **git branch -d [브랜치 이름]** : 기촌 브랜치 삭제
- **git checkout [브랜치 이름]** : 기존 다른 브랜치로 이동
- **git merge [브랜치 이름]** : 현재 브랜치에 해당 브랜치를 합침
- **git merge --abort** : merge를 하다가 confict(충돌)가 발생했을 때 취소하고 돌아감
- **git fetch** : 로컬 레파지토리에서 현재 HEAD가 가리키는 브랜치의 upstream branch로 부터 최신 커밋들을 가져옴
- **git blame** : 특정 파일의 내용 한줄한줄이 어떤 커밋에 의해 싱긴 것인지 출력
- **git stash** : 작업 내용을 임시로 저장
- **git stash list** : 임시로 저장된 작업 내용을 조회
- **git stash apply [?작업 내용의 아이디]** : 생략하면 가장 최근의 작업 내용이 적용
- **git stash drop [?작업 내용의 아이디]** : 생략하면 가장 최근의 작업 내용이 삭제
- **git stash pop** : 기존 리스트의 임시저장 내용 적용과 동시에 스택에서 제거
- **git cherry-pick [커밋아이디]** : 필요한 커밋만 가져옴