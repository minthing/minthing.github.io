---
title: "깃허브 블로그 만들기 그 험난한 여정 🛤"
categories:
  - blog
tags:
  - blog
---

예전 windows를 썼을 때 부터 깃허브 블로그는 나에게 애증의 존재였다.
그 때는 지금보다 개발 실력이 없는 진짜 뉴비중의 뉴비여서 에러 해결 방법도 구글 검색 방법도 몰라서 결국 로컬 서버 확인 없이 일단 서버에 띄우고 확인한다는 미친 짓을 벌이기도 했다.

하지만 왜 나는 기업에서 잘만 관리해주고 코드 에디터도 잘만 달려 있고 광고까지 달 수 있는
티스토리 블로그를 잘만 쓰다가 어찌하여 깃허브 블로그를 다시 사용하기로 했는가.

일단 이 지킬이란 놈을 나만 잘 못쓰나? 라는 의문이 들었다.
두번째로, 티스토리 블로그에 글을 올리기 위해 기껏 작성한 코드와 이미지들을 수정하기도 귀찮고 되도록 vscode에서 직접 관리하고 싶었다.
그리고 깃허브 연동이 된다! 잔디🌱를 심기 위해서! 그냥 이론 공부만 했을 때 막상 깃허브 커밋이 안들어가면 왠지 공부해도 공부 안한 것 같고 가끔 느끼는 것만 정리하고 싶을 때 나만의 블로그가 가지고 싶었다.

그러나 이 여정 결코 쉽지 않았음을 나는 몰랐다. 지금은 오후 11시 35분. 내가 블로그를 파야지 하고 시작했던 시각에서 벌써 3시간이나 지나있다.

* 맥 OS Big Sur 환경 > windows는 따라하다가 잘 안될 수 있음.
* 사용하는 템플릿은 [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)이다.


<!-- ### Task Lists

- [x] Finish my changes
- [ ] Push my commits to GitHub
- [ ] Open a pull request
  - [ ] Follow discussions
  - [x] Push new commits -->

## 기본적인 지킬 블로그 생성 방법

  먼저 `사용자아이디.github.io`라는 타이틀을 가진 레파지토리를 생성해야 한다.

  ![image](https://user-images.githubusercontent.com/54466684/133532161-0bb4070a-5076-4c03-9af5-fb21a423a9e8.png)

나는 이미 `minthing.github.io`라는 레파지토리가 생성되어 있기 때문에 빨갛게 뜨지만 처음 생성하는 분들은 정상 노출 될 것이다.

이 과정을 완료했다면 생성된 레파지토리를 로컬로 클론 해준다.

나는 가장 먼저 `README.md` 파일을 생성하여 다음과 같이 작성했고 이것을 푸쉬하면 정상적으로 사이트에 반영이 되는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/54466684/133532640-ea4d56df-c8a0-45ec-86ae-f6d491525382.png)

* 반영된 모습 

![image](https://user-images.githubusercontent.com/54466684/133532609-e80105e5-928f-4b63-9e2b-a7a54aa54125.png)

여기까지 따라왔다면 이제 템플릿을 씌워 줄 차례다. 우리가 사용할 [minimal-mistakes](https://github.com/mmistakes/minimal-mistakes)로 가서 해당 파일을 zip 파일로 다운 받고 README를 제외한 모든 파일을 로컬 레파지토리에 복사 붙여넣기 해준다.

![image](https://user-images.githubusercontent.com/54466684/133532815-c805d56d-e97a-4f0f-adf2-3ccb4ecc2bdf.png)

이제 이것을 로컬에 띄워야 하는데 여기서부터 문제가 많다.

만약 블로그 폴더 상에서 터미널에 다음 문구를 입력했을 때 정상 동작한다면 끝이지만, 아니라면 아래를 참고 부탁한다.

```
gem install bundler jekyll // 번들러 및 지킬 설치
bundle exec jekyll serve // 서버 실행
```

* 정상 동작할 때 터미널

![image](https://user-images.githubusercontent.com/54466684/133533084-d078d252-9bfd-4ee3-8791-3646366b07f5.png)


* 에러 발생 시

![image](https://user-images.githubusercontent.com/54466684/133533184-71691355-1f77-40a8-aa07-7d18b6735dee.png)

먼저 이 에러가 발생했다면 ruby가 있기는 있는데 시스템에서 사용하는 루비만 있기 때문에 안되는 것이다.


### homebrew는 설치 되었나요?

  맥북유저라면 homebrew가 설치되어 있어야 한다. 부끄럽게도 나는 지금 다니는 회사에 입사하기 전 windows 환경에서만 개발을 해 봤기 때문에 homebrew가 뭔지, 왜 필요한지도 알지 못했고 그나마도 사수가 맥북 세팅해주면서 설치해 주셨다.

  그러나 개인 맥북이 생긴 지금 homebrew 없이 개발하기 힘들다는 사실을 잘 안다. 맥북 명령어는 대부분 `brew`를 타기 때문에 `npm` 명령어를 찾으려면 내가 또 뭔가 검색해야 한다.

  * homebrew 설치 명령어

  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  ```

설치가 완료 되었다면 enter 키를 눌러주자. 난 이것도 몰랐는데 return 키가 enter 키더라...

그 다음 password를 입력하라고 나오는데 그 때 맥북 켤 때 사용하는 password 입력해주면 된다.

정상적으로 모든 설치가 완료 되었다면 다음 명령어를 쳐준다.

##### cask 설치

이건 당장 필요 없어도 나중에 유용해진다. chrome 같은 걸 명령어로 설치 가능해짐.

```
brew install cask
```

### 루비 버전을 확인하자.

먼저 맥북 유저라면 다들 `python`, `ruby`가 설치되어 있다.

`ruby -v` 했을 때 이미 설치된걸로 뜬다. 그러나 방심하면 안된다. 예전에 `django`공부할 때 이미 `python` 설치 된 거 보고 "오, 이미 설치가 다 되어있네. 역시 맥북! 개꿀! 👍" 이러고 넘어갔고 정상적으로 동작했다.

그러나 `ruby`는 다르다. 만일 당신이 다음과 같은 에러를 만났다면 당신 맥북에 있는 `ruby`는 시스템에서 사용하는 것이므로 새로 설치해 주어야 한다.

```
% gem install bundler Fetching bundler-2.2.15.gem

ERROR: While executing gem ... (Gem::FilePermissionError) You don't have write permissions for the /Library/Ruby/Gems/2.6.0 directory.
```

우리는 방금 전 homebrew 설치를 마쳤기 때문에 다음 명령어를 쳐준다.

```
brew update
```

그 다음 루비를 재설치 해주자.

```
brew install rbenv ruby-build
```

루비 버전을 확인했을 때 `system`하나만 있다면 다른 버전의 루비 설치가 필요하다.

```
rbenv versions
```

![image](https://user-images.githubusercontent.com/54466684/133533446-8c3de7f2-d57c-40db-94ea-994ef018d982.png)

루비 2.7 버전 설치하기
```
rbenv install 2.7.2
```

설치를 완료한 후에 다시 `rbenv versions`로 확인해 보면 다음과 같이 뜰 것이다.


```
* system
2.7.2 (set by /Users/{{username}}/.rbenv/version)
```

`*`이 붙어 있는 게 지금 사용중인 루비 버전이라는 뜻이므로 우리는 이 별을 우리가 방금 설치한 루비 버전으로 옮겨줘야 한다.

아래 명령어를 통해 우리가 글로벌로 사용할 루비 버전을 변경해준다.

```
rbenv global 2.7.2
```

이 다음 다시 루비 버전 확인을 해보면 별 위치가 옮겨진 것을 볼 수 있을 것이다.


```
system
* 2.7.2 (set by /Users/{{username}}/.rbenv/version)
```

이제 다음 명령어를 쳤을 때 정상 동작해야 한다.

```
gem install bundler jekyll
```

근데 안 될 수도 있다. 또 다시 permission 이슈가 발생한다면 다음 [글](https://github.com/rbenv/rbenv/issues/1207)을 참고하자. 근데 나는 재부팅하니까 된다.

이 다음 서버를 실행했을 때 정상 동작하면 되는데 안된다면 bundler 버전 이슈일 가능성이 있으니 확인하자.

```
bundle exec jekyll serve
```

에러 발생 화면

![image](https://user-images.githubusercontent.com/54466684/133534588-8acd6e54-490d-48c4-9c97-1851d1421ee8.png)

하라는 대로 다음 명령어를 통해 해결하자. 나는 업데이트 두 세번 해야 서버 정상 동작 했음.

```
bundle install
bundle update
```

### config 파일을 수정해 보자.

로컬 서버를 띄우는 데 성공했다면 이제 꾸미는 일만 남았다. 우리가 사용한 지킬 블로그 템플릿은 다양한 기능을 제공하므로 하나씩 알아보도록 하자.

가장 먼저 `_config.yml` 파일을 수정하여 블로그의 기본적인 틀을 잡아보자.

```yml
# 블로그 배경 색을 정할 수 있습니다.
minimal_mistakes_skin    : "dirt" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"

# Site Settings
locale                   : "ko-KR" # 언어 설정 바꾸기
title                    : "minthing's blog" # 블로그 타이틀
title_separator          : "-"
subtitle                 : # site tagline that appears below site title in masthead
name                     : "minthing" # 블로그에서 사용되는 이름
description              : "내가 하는 일이 나를 정의한다 ✨."
url                      : "https://minthing.github.io" # 블로그 url
baseurl                  : #/blog
repository               : "https://github.com/minthing/minthing.github.io"
```

좀 더 하단으로 가면 작성자 정보를 입력할 수 있다.

```yml
author:
  name             : "minthing"
  avatar           : "/assets/images/avatar.jpeg" # 내 캐릭터
  bio              : "💻 개발자는 성장중"
  location         : "korea"
  email            :
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      #url: ""
    - label: "Website"
      icon: "fas fa-fw fa-link"
      url: "mber.tistory.com"
    # - label: "Twitter"
    #   icon: "fab fa-fw fa-twitter-square"
    #   # url: "https://twitter.com/"
    # - label: "Facebook"
    #   icon: "fab fa-fw fa-facebook-square"
    #   # url: "https://facebook.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/minthing"
    # - label: "Instagram"
    #   icon: "fab fa-fw fa-instagram"
    #   # url: "https://instagram.com/"

```

그 다음 카테고리를 지정해 줄 겁니다. `_data/navigation.yml`을 수정해보자

```yml
# main links
main:
  - title: "👋"
    url: /about/
  - title: "🗃"
    url: "/categories/"
  - title: "🏷"
    url: /tags/
```

이제 나머지는 css 등 자기가 원하는 대로 커스터마이징 해주면 됩니다! 로컬 환경에서 블로그를 열어 테스트 한 후 배포하면 일단 끝이다.

`test/_pages` 또는 `test/_posts`등을 참고하시면 도움이 될 것이다.