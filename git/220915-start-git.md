##Index
- git flow
- Hexo

### branching models

- git flow : 개발 팀이 씀. release 할 수 있는 권한이 생기기 전까지 develop 과 feature branch 를 사용한다고 함. main과 develop branch 를 나눠서 쓴다는 것이 특징. main branch 의 모든 commit 단위들은 실제로 쓰이는 것들.(clients 에서 동작하는 것들) main branch 는 commit 을 직접적으로 하는 공간이 아니다 라는 점을 알고 있자. 긴급한 버그들은 hotfix(긴급 수정)에서 긴급 수정을 거쳐서 main으로 바로 넘긴다고 함. web, app team 단위에서 많이 쓴다.
- github flow : 개발하고 집어넣으면 바로 반영됨. library 팀들이 많이 쓴다고 함. frameworks 나 lang 팀도.
- gitlab flow : github flow 랑 비슷.

### git flow strategy

- feature branch를 따서 작업 후 develop 에 밀어넣음. 안전적인 개발에 좋음.

### git flow 를 사용하면 쉽게 git 할 수 있다.

- [https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html](https://danielkummer.github.io/git-flow-cheatsheet/index.ko_KR.html)

```jsx
**$ brew install git-flow-avh**
```

설치가 완료되었으면 git flow 를 사용해보자.

- .gitignore 을 main branch 에서 미리 셋팅, issues 도 clone 후 미리 셋팅.
- .gitignore touch로 만들고 vi 로 편집 후 저장. add, commit (config: Create .gitignore)

- main branch 에서

```jsx
$ git flow init
```

```jsx
$ git flow feature start {name}
```

⇒ feature branch 로 switch

파일을 추가 및 수정 후 add - commit 까지 마쳤다면 아래와 같이 입력.

```jsx
$ git flow feature finish name
```

⇒ feature branch 는 삭제 되어지고 develop brunch 로 자동 switch 됨.

> 버전 release 할 때는 보통 v0.1 과 같이 두자릿수로 함.
>

> 앞의 숫자가 0일 때는 보통 beta 버전임. 1→2 로 넘어갈때는 두 버전 사이의 호환이 불가능 할 때라고 한다.
>

```jsx
$ git flow release start v0.1
```

```jsx
$ git flow release finish v0.1
```

⇒ develop branch 와 main branch 로 각각 Merge commit 되어 들어감.

release branch 사라지고 develop branch 로 switch 되어진다.

✋ push 명령어는 develop과 main 에서 한번씩 해주면 된다.

- develop 에서 push

```jsx
$ git push -u origin develop
```

⇒ github 에 실제로 보면 branch 가 main 밖에 없는 것을 확인할 수가 있다. 하지만, 우리는 여태 로컬의 develop 에서 작업을 했고, develop은 remote 에서 쓰는 main과 형태가 같음을 알려준다. 라는 명령어로 이해하면 되겠다.

- main 에서도 push

```jsx
$ git push origin main
```

1. tag 만들어진것도 push 해야함. (릴리즈 노트 작성한 것)

```jsx
$ git push tags
```

⇒  위 명령어가 실행되지 않아서 main branch 에서 $ git push origin —tags 로 작업하였다. (모든 태그들을 다 push 하는 방법이라고 한다..)

Static Site 만들기. (Static Site Generator을 이용하기.)

- Jekyll : Ruby 기반의 정적인 블로그 생성기.
- Hugo : Golang 기반의 정적인 블로그 생성기.
- Hexo : Node.js 기반의 정적인 블로그 생성기.  가장 쉬우므로 Hexo 로 시작해보자.

```jsx
$ brew install node
```

```jsx
$node -v
```

```jsx
$npm -v
```

⇒ 위 명령어로 설치가 잘되었는지 확인해보자.

설치가 잘 되었다면 [https://hexo.io/](https://hexo.io/) 로 이동하여 보자.

Docs - Getting Started 으로 확인해보면

- npm
- git

이 최소한 깔려있어야 한다고 기재되어있다.

아래 명령어를 사용해서 설치.

```jsx
$ sudo npm install -g hexo-cli
```

⇒ g 는 global

⇒ mac 권한이 필요하기 때문에 sudo 필수로 입력해서 설치한다.

```jsx
$ hexo
```

⇒ 명령어를 실행해서 잘 설치 되었는지 확인.

dev폴더로 와서

```jsx
$ hexo init {이름}
```

나는 $ hexo init jjonglog 로 하였다…ㅎㅎ

$ ls

package.json - 중요파일

_config.yml - 환경설정 파일이므로 중요파일

$ npm install

⇒ 빠진게 있는지 설치 한번 해주기.

## **new**

```
$ hexo new [layout] <title>
```

---

⇒ 기본은 post / 제목은 “” 안에 넣어주자. “”는 30자 이내로 작성할 것. 공들여서 썼는데 검색이 안될 수도 있으니까 seo를 신경쓰자.

실행하고 나면 절대 경로가 뜬다.

참고해서 vi 편집기로 md 파일을 열어보자.

title 을 한글로 변경해도 된다. url 은 영어로 되어있을 것이다.

tags 는 - 를 이용해서 달아주면 된다.

## **generate**

```
$ hexo generate

```

---

편집기에서 다 작성했으면 :wq 로 저장하고 위 명령어로 생성해주자.

## **server**

```
$ hexo server
```

---

로컬에서 확인하기

[http://localhost:4000/](http://localhost:4000/) 에서 작성한 글을 확인해보자!

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7cf2040e-cdb1-4c7b-b0e3-1f00111d2a89/Untitled.png)

제법 멋지죠?

서버를 중단하려면 Ctrl+C 로 서버를 중단시키면 된다.

로컬이 아닌

[devSojoong.github.io](http://devsojoong.github.io/) 로 New Repository 만들어준다.

(나는 이미 있어서 안함.)

Deployment - one command Deployment

Tool 설치.

```jsx
$ npm install hexo-deployer-git —save
```

_config.yml 수정.

- timezone 이나 language 는 가급적이면 수정하지 않는 것이 좋다. 테마에 따라 깨질 수도 있기 때문이다.
- url 을 수정해준다. [https://devsojoong.github.io](https://devsojoong.github.io) 로 수정해준다. (마지막에 / 해주는 행동은 하지 말자.)
- deploy :

    type: git (다음에 설정할 것.)

    (: 뒤에 공백 꼭 붙여주기 아니면 syntax 깨짐.)

    repo: repo 주소 복붙 (다음에 설정할 것.)

    branch: main (다음에 설정할 것.)


설정이 다 끝났으면 아래 명령어 실행해주기.

```jsx
$ hexo clean && hexo generate
```

```jsx
$ hexo server
```

⇒ 제대로 수정됐는지 확인 Command +Shift + R (cash clear 후 새로고침)

```jsx
$ hexo deploy
```

⇒ url 을 입력하면 로컬에서 봤던 화면이 그대로 뜨게 된다.

테마 변경해보기

- Theme - NexT 테마 적용해보기.

```jsx
$ npm install hexo-theme-next —save
```

설치가 되었다면

```jsx
$ vi _config.yml
```

theme 을 next로 변경해주자. (theme : next)

```jsx
$ hexo clear && hexo generate
$ hexo server
```

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f7c43e14-7a2a-4000-849b-0db5a3b28c96/Untitled.png)

바꾼 테마가 훨씬 낫다!

```jsx
$ hexo deploy
```

까지 마무리 해주면 된다.

Repository 에서 commit 된 거까지 확인해보기!
