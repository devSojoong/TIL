# index

- Working directory 에서 작업 되돌리기
- Stage 에 있는 작업 되돌리기
- git flow 를 활용한 Collaborate git 하기.

### working directory 에서 작업 되돌리기

- Shell 에서 파일의 이름 바꿀 때 Command (rename)

```jsx
$ mv 기존파일명.확장자 변경할파일명.확장자
```

⚠️ git 에서는 이 방법으로 하면 안된다.

왜냐하면, 기존 파일이 delete 되고, 새로운 파일이 새로 생긴걸로 tracking 하기 때문이다.

✋ 기존 Shell Command 방식으로 파일명을 변경했다면 아래를 참고하자.

1. 다시 아래 명령어로 파일명 변경 이전 상태로 복구한다.

```jsx
$ mv 변경된파일명.확장자 기존파일명.확장자
```

1. 아래 명령어와 같이 다시 파일명 변경해준다.

```jsx
$ git mv 기존파일명.확장자 변경할파일명.확장자 
```

위 명령어까지 실행하게 되면 $ git status 했을 때 rename 되었다고 보이고, (물리적인 변화는 없기 때문이다.) working tree가 깨끗해진다. 그리고 add 를 하지 않아도 되는 상태이기 때문에 commit 으로 바로 진행해주면 되겠다. (prefix: fix)

- undo

파일을 저장까지 이미 마친 상태에서 마음에 들지 않을 때 최신 commit 으로 되돌려보자. (add 이전의 상태여야함)

```jsx
$ git restore 파일명.확장자
```

여러개의 파일을 한꺼번에 되돌리기

```jsx
$ git restore .
```

- Unstaging (stage 에 올린거 되돌리기)

git add 된 상태에서 (commit 이전에서) 되돌리고 싶을 때

```jsx
$ git resert HEAD 파일명.확장자
```

> HEAD : 최신의 상태
> 

- 수정한 파일이 두 개 이상일 때

doc 과 feat 작업단위가 각각 있을 때(=commit 이 각각 일 때)

stage 에 있는 한가지의 작업을 우선 내려보자. (ex [README.md](http://README.md) 파일)

```jsx
$ git resert HEAD README.md
```

- Commit

commit 은 blob 과 tree 로 나뉘어져있다.

add 와 commit 을 진행했을 때(tree 부분을 수정) commit 메세지를 엉망으로 한 경우 어떻게 해야할까?

- 가장 최신의 commit 메세지를 수정할 때

```jsx
$ git commit --amend
```

명령어 실행 후 다시 입력 후 :wq

```jsx
$ git log 
```

로 수정된 내용 확인해보자.

**⇒ 위 내용들은 Push 전에만 가능한 것들…이라고 한다…**

### Reset commit

Commit 이 잘못된 것도 삭제하지 않고 이력 관리 용으로 남겨야한다고 한다.

- reset : commit 남김없이 없앤다.
- revert : 잘못된 점을 바로 잡기.

결론, reset 은 지양하자….

Best case : Revert ! 👍

ex) 잘못된 파일 이력 3가지를 만들었는데 commit 까지 마쳤을 때 발생되기 전 이전으로 돌려보자.

```jsx
$ git lg 
```

⇒ 위 명령어로 확인해보면 잘못된 commit 3가지 확인이 가능하다.

```jsx
$ git revert —no-commit HEAD~3..
```

⇒ 최신의 상태부터 3개를 편집기 창 띄우지 않고 한번에 commit 할게 라는 뜻.

```jsx
$ ls
```

⇒ 확인해보면 만든 파일들 사라져있음…!🙀

```jsx
$ git status
```

⇒ 사라진 파일 세가지가 commit 이전의 상태임을 확인할 수  있다.

```jsx
$ git commit
```

⇒ 다시 commit 하면 편집기가 뜨고 commit message 재작성 가능하다.

```jsx
$ git lg 
```

⇒ 이전의 잘못 업로드 되어 올라간 commit 들도 보이지만 제대로 수정되어 올라간 history 도 생성된 것을 확인할 수 있다.

> 🙌  잘못하기 전 과거로 돌아가 최신을 유지하면서 되돌렸다 라는 이력을 commit 으로 남겨 모든 팀원이 이 사항을 공유할 수 있다.
> 
- commit 을 따로 안할 땐 —no-edit
- merge commit 을 되돌릴 땐 -m($ git revert -m {1 or 2} {merge commit id})

### Collaborate git

- git flow 와 workflow 를 활용.

### 🐯 팀장이 해야하는 일

1. github 에서 + 버튼을 누르고 new organization을 만들어준다.
2. Your organization 으로 이동. people 탭에서도 초대가 가능하다.
3. Repositories 에서 repo 생성하기.
4. repo 명 작성 - public 으로 체크.
5. Issues 템플릿을 작성해야함.(New issues). 여러 문제들을 list up 하는 공간.
    - Settings - Features - 이슈 템플릿 만들 수 있다. (bug, custom issues 등을 edit 해서 작성 가능.) ←먼저 해야함.
6. 셋팅 후 url 전달 받아서 로컬에서 clone 해오기.
7. 해당 repo directory 로 이동해서 branch 와 대상파일 setup 해주기.
    - $ git flow init
    - $ git branch
    - 파일 생성 (동작까지 하는지 확인 후 commit 올려야한다. 불완전하면 절대 안된다.)
    - $ git add 파일
    - $ git commit  (prefix : feat)
    - 로컬에서 develop 을 처음 만들었기 때문에 git push -u origin develop 으로 develop branch 에서 해줘야함. (그래야 main 이랑 형태가 같은 branch 임을 인식하기 때문.)
    - 대상 파일 생성 후 origin develop 으로 push
    

### 🐱 팀원이 해야하는 일

1. issues 에 내가 해야할 일을 먼저 적어놓고 작업 시작하기.
    - issues 선택 후 get started 하고 form 을 채우기. (github 의 문서는 markdown 으로 이루어져 있다.)
2. develop 확인 후 fork 
    
    ⇒ direct push 가 들어오는 경우 방지.
    
    2-1. copy the main branch only 해제 (develop에서 작업할 것이기 때문에)
    
    2-2. fork  설정 시 사본을 내가 갖고 있는 것과 같다. (내 권한으로 하나 생김)
    
3. 내 repo 방문 전 organization에서 내 할 일 issue 에 등록
4. 로컬에 fork clone 가져오기.
5. git flow init 
6. git flow feature start 이름 
7. 파일 추가 및 수정 등의 작업 이후 add , commit
8. git flow feature finish 이름
9. git push - u origin develop
10. Open pull request
- pull requests 작성할때는 내 fork repo 에서 작업해주어야한다. (자주 헷갈림…)
- ⚠️ 내 fork repo develop에서 pull requests 해주기. fork repo develop 에서 작업한거 ⇒ 실제 repo develop 에 pull 해줘야함. (branch 확인 잘하기)
- requests 내용 작성할 때 ex) resolve #1 해주면 자동완성으로 기존에 작성한 issues를 땡겨올 수 있음. (resolves, resolved, fix, close 등등 /  입력 시 preview가 뜬다. )

### 🐯 팀장이 해야하는 일

1. Code review (pull requests에 댓글 확인.)

### 🐱 팀원이 해야하는 일

1.  팀장의 Code review 에 따라 추가 작업 후 origin develop 으로 push 하기.
2. Merge Conflict 가 있다면 조직의 develop을 local 로 pull하여 conflict 해결 후 add, commit, push 해주기.
    - 수정이 반영된 내용을 가져오고자 할 때는

```jsx
$ git remote add 해당사용자별칭지정 주소
```

⇒ 내 로컬로 해당 별칭 원격저장소 땡겨올 수 있음.

Tip. 원격 저장소 별칭 잘못 줬을 때 지우고 다시 하기

```jsx
$ git remote remove 별칭
```

```jsx
$ git remote add 별칭 원격저장소주소
```

$ git pull 별명 develop

- $ git pull 했는데 안된다니까요..? 🤷‍♀️🤷‍♀️🤷‍♀️🤷‍♀️🤷‍♀️🤷‍♀️….. (꿀팁보장 주의💢)
    
    ```jsx
    $ git pull 별칭 develop
    ```
    
    pull 했을 때 merge conflict 안뜨면 아래와 같이 fetch 로 실행해보자.
    
    ```jsx
    $ git fetch 별칭 develop 
    ```
    
    ### 🤔 fetch vs pull
    
    fetch 는 해당 원격저장소의 변경된 사항이 있는지 없는지 체크만 하는 용도 로컬 git 에 반영해주지 않는다.
    
    pull 은 해당 원격저장소의 변경된 사항이 있으면 최신 데이터를 복사하여 로컬 git으로 가져오는 작업까지 해준다.
    
    > 출처: [https://www.freecodecamp.org/korean/news/git-fetch-vs-pull/](https://www.freecodecamp.org/korean/news/git-fetch-vs-pull/)
    > 
    
    > `git fetch`를 사용하면 마지막 `pull`이후 원격 저장소 또는 브랜치에 적용된 변경 사항을 확인할 수 있습니다. 만일 원격 저장소에 변경 사항이 존재하는 상황에서 `pull`을 바로 실행하면 현재 브랜치와 작업 복사본의 파일이 변경되는 동시에 새로 작업한 내용이 손실되는 일이 생길 수 있습니다.                따라서 `fetch`로 변경 사항을 먼저 확인한 후 `pull`을 실행하는 방법이 보다 안전합니다.
    > 
    
    ⇒ pull 로 merge conflict 해결 하려고 했을 때 
    
    ```jsx
    sojoongyoon@SOJOONGui-MacBookAir black % git pull blackjack develop
    remote: Enumerating objects: 19, done.
    remote: Counting objects: 100% (19/19), done.
    remote: Compressing objects: 100% (11/11), done.
    remote: Total 15 (delta 8), reused 10 (delta 4), pack-reused 0
    오브젝트 묶음 푸는 중: 100% (15/15), 2.60 KiB | 177.00 KiB/s, 완료.
    [https://github.com/kdt-blackjack/black](https://github.com/kdt-blackjack/black) URL에서 
    branch develop -> FETCH_HEAD
    c2161e9..496ed30 develop -> blackjack/develop
    힌트: You have divergent branches and need to specify how to reconcile them.
    힌트: You can do so by running one of the following commands sometime before
    힌트: your next pull:
    힌트:
    힌트: git config pull.rebase false # merge
    힌트: git config pull.rebase true # rebase
    힌트: git config pull.ff only # fast-forward only
    힌트:
    힌트: You can replace "git config" with "git config --global" to set a default
    힌트: preference for all repositories. You can also pass --rebase, --no-rebase,
    힌트: or --ff-only on the command line to override the configured default per
    힌트: invocation.
    fatal: Need to specify how to reconcile divergent branches.
    ```
    
    위와 같은 오류 발생하면서 원격저장소에 있는 최신 파일을 가져오지 못했다.
    
    ```jsx
    $ git fetch blackjack develop
    ```
    
    을 실행해주었더니 아래와 같이 확인되었고,
    
    ```jsx
    [https://github.com/kdt-blackjack/black](https://github.com/kdt-blackjack/black) URL에서 
    branch develop -> FETCH_HEAD
    ```
    
    ```jsx
    $ git merge FETCH_HEAD
    ```
    
    ⇒ 위 명령어로 병합 충돌 되는 파일과 자동 병합이 실패했음을 마침내 확인할 수 있었다. (아래 확인)
    
    ```jsx
    sojoongyoon@SOJOONGui-MacBookAir black % git merge FETCH_HEAD
    자동 병합: [blackjack.md](http://blackjack.md/)
    충돌 (내용): blackjack.md에 병합 충돌
    자동 병합이 실패했습니다. 충돌을 바로잡고 결과물을 커밋하십시오.
    ```
    
    vi 편집기를 열어 파일을 수정하고 add, commit 후 내 fork repo의 develop 으로 push 해주었다.
    
    ```jsx
    $ git push origin develop
    ```
    

내가 골라서 받아와야할 때는 fetch & merge 가 가능하다.

```jsx
$ git fetch 별명 develop 
```

```jsx
$ git merge FETCH_HEAD
```

⇒ fetch branch 에 임시로 merge를 받는다.

### 🐯 팀장이 해야하는 일

1. Merge pull request
2. 

```jsx
$ git flow release start v0.1
```

11.

```jsx
$ git flow release finish v0.1
```

12.

develop 에서 

```jsx
$ git push origin develop
```

main 에서 

```jsx
$ git push origin main
```

13.

```jsx
$ git push origin --tags
```

1. github 에서 tags generate 해주기.
