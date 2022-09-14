# TIL

Today I Learned (22/09/14)


## Index

- What is git?
- Linux Command
- How to use vim
- Mac os -> git installation
- github -> add, commit, push


## What is git?

- git은 원격 저장소.  프로젝트 이슈 관리가 용이하며  타인과 협업 시  다른 프로젝트에 기여할 수 있다라는 점이 가장 크다.


## Linux Command
~%  : 권한 없이 사용할 수 있는 최상의 위치임을 알려줌.

ls : list segements 현재 위치 아래로 사용할 수 있는 파일 디렉토리 리스트.
- ls -a : 숨김 파일 까지 다 보임.
- ls -l : 상세 정보까지 다 볼 수 있음.
- ls - la 도 가능.

cd : cd 디렉토리/ 하면 해당 디렉토리 경로로 현재 위치 변경된다.


. : 현재 디렉토리
.. : 상위 디렉토리


mkdir 파일이름  :파일 생성

명령어와 명령어 사이의 구분자는 스페이스이다.


git 사용의 주 목적은 파일 관리임.

touch 파일명.확장자 :  touch readme.txt 로 하면 텍스트파일 기반의 readme 파일이름을 가진 파일을 생성할 수 있다.

mv : 파일 이동하는 명령어.

cp : 파일 복사하는 명령어.
cp 파일명 : 파일명 그대로 복사해서 똑같이 생성된다.
cp 파일명 새로운 파일명 : 복사하고자 하는 파일명의 새로운파일명으로 새로 만들어짐.


delete : 파일 껍데기 삭제하기 , 물리적으로 남아있음.
remove : 파일 완전히 삭제하기


rm : 파일 삭제 하기

와일드 카드 (*)

rm *.go : .go 확장자를 가진 파일을 지워라.
rm server.* : Server라는 파일명을 가진 파일을 지워라.

rm 으로 디렉토리 자체를 삭제는 불가하고 파일만 지울수 있고
디렉토리 지우려면 rm - r 이라는 옵션을 주어야함.

/Users/sojoongyoon : 터미널 켰을 때 최상위 디렉토리

cat : 파일 상태 체크하기 위한 명령어(편집모드로 들어가지 않음.)


## How to use vim


i : insert 모드로 변경된다.
ESC : normal 모드
V : visual 모드(보통 블럭 잡을때 쓴다고 함)
: 는 command 모드

### Vim commands

- hjkl - Arrow key
- y - yank(shift + y 한줄 복사 / shift + p 한줄 붙여넣기)
- p - paste
- d - delete


## Mac os -< git installation

1. homebrew 를 우선 설치.
2. $ brew install git
3. $ git --version
 

## github -> add, commit, push

- commit 단위로 수정내용을 관리 (time stamp), 배포 뿐만 아니라 원하는 시점으로 체크아웃 가능.

<중요>
- git Process Flow and Command 
(add - commit - push)


Local 의 commit 이 어느정도 쌓였을 때 push 함.

git 과 github (remote 의 역할 +GitLab)는 다르다.


cd 만 실행하면 최초 디렉토리로 돌아옴.


우선 git config 해주기.


New Repository (새로운 원격 저장소)

git clone 해서 로컬에 만들어줌.


readme 는 대문글 (features)

readme.md 수정 후 저장
git add -> git commit 

후 1번 라인에 제목 3번 라인에 내용 입력 후 저장 

그 다음에 push 하려면

github settings 에서 developer settings


토큰 만들고

git push origin main


username 입력후 pwd 에 토큰 복붙 후 엔터



example 1) 새 파일을 만들어서 오늘 먹고 싶은 음식 세가지 입력해서 commit push

$ touch menus.md

$ vi menums.md

##blablablaabl

1.
2.
3.

:wq

$ git status

$ git add menus.md

$ git commit

Edit menus.md

writing what i want to eat dinner today


:wq

$ git status

$ git push

여러 수정을 한번에 커밋하려고 할때 
시간 단위로 분류해서 논리적 흐름에 따라 커밋을 해도 된다고 함.

먼저 한 작업을 git add 파일명 해줌.
git status 로 확인 가능.

첫번째 작업 git add - git commit 
두번째 작업 git add - git commit

마지막 push

commit 할 때 내용 적을 때 conventional commits prefix 지켜서 해주기.

feat
fix
docs
test
conf


gitignore.io 에서 내가 사용하는 것들 셋팅 되어있어서 해당 내용들 복사해서
vi .gitignore 에 추가 함. git add / git commit / git push

라이센스는 학습용으로 쓸 수 있는 MIT 라이센스를 쓰자.

클론을 사용해서 repository 만드는 방법

repo 만들고 git clone 주소복붙


directory 만 만들어서는 path 가 개념적으로만 존재하고
git status 했을 때는 commit 할게 없다고 함.


git status -uall 하면 해당 경로 이하의 자세한 내용들이 보인다.

