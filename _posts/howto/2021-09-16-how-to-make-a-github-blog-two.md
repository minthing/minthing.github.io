---
title: "깃허브 블로그 만들기 그 험난한 여정 (2) 🛤 - 커스터마이징 및 포스팅 하기"
categories:
  - howto
tags:
  - jykll
  - blog
---

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

좀 더 하단으로 가시면 작성자 정보를 기입할 수 있습니다.

```yml
author:
  name             : "minthing"
  avatar           : "/assets/images/avatar.jpeg" # 내 캐릭터
  bio              : "💻 & 📖 & ✍️"
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

그 다음 카테고리를 지정해 줄 겁니다. `_data/navigation.yml`을 수정해 줍니다.

```yml
# main links
main:
  - title: "👋"
    url: /about/about/
  - title: "🗃"
    url: "/categories/"
  - title: "🏷"
    url: /tags/
```

이제 나머지는 css 등 자기가 원하는 대로 커스터마이징 해주면 됩니다! 로컬 환경에서 블로그를 열어 테스트 한 후 배포하면 됩니다. ✨

`test/_pages` 또는 `test/_posts`등을 참고하시면 도움이 될 겁니다.