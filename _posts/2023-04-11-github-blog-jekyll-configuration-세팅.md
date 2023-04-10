---
layout: post
title: "[Github blog] jekyll configuration 세팅"
date: 2023-04-11 01:02 +0900
subtitle: 기본적인 Jekyll의 configuration을 세팅해보자
category: [Web, blog]
tags: [github blog, blog, jekyll, chirpy, jekyll-compose, jekyll plugin]
---

## Jekyll의 configuration을 세팅해보자 

기본적인 블로그를 세팅하기 위해 여러 가지 기본 configuration을 세팅해주어야 한다. 이를 위해선 `_config.yml`{: .filepath}에서 수정을 해주어야 한다.

수정한 부분은 아래와 같다. 
```yaml
lang: ko-KR 
timezone: Asia/Seoul 
title: erin 🩵
tagline: erin's blog
description: Erin's github blog.
url: "https://lalalse.github.io"
github: 
  username: lalalse
social:
  name: erin
  email: lalalse96@gmail.com
  links:
    - https://github.com/lalalse
img_cdn: "https://user-images.githubusercontent.com/{user_number_id}"
avatar: "230730891-c071edbe-2824-4ef2-a373-12a3f3895b13.png"
```

우선 언어를 ko-KR로 바꿔줌으로써 한글로 바꿔줬다 ! 지금은 이렇게 했다가 나중에 다시 영어로 돌릴 것 같긴 하지만 우선은..?😉 
그 외에 title, tagline, description 같은 부분은 간단하게 erin의 블로그라는 내용만을 가득 담아서 작성했다.
이후에 이런저런 github link를 포함한 social link들을 수정해주었다.


## img_cdn 설정 및 블로그에 이미지 업로드하기 
여기서 내가 생각하기에 가장 중요한 부분은 바로 이 부분이다.

```yaml
img_cdn: "https://user-images.githubusercontent.com/{user_number_id}"
```
당연히 게시글을 작성하다 보면 이미지를 넣을 일들이 무궁무진하다. 
그러나 이 이미지들을 어떻게든 서빙할 수 있도록 만들어줘야 하는데, 내가 생각하기에 가장 손쉬운 방법은 github에서 제공해주는 기능을 사용하는 것이다. 

github repository에서 Issues -> 이미지를 복사붙여넣기하면 github에서 이 이미지를 서빙하기 위해 자신들의 데이터베이스에 올려놓게 된다. 
![예시 이미지](/230942916-df057c73-67cf-4f52-891c-16a69bcd9de9.png)

이렇게 이미지를 업로드하면 src에 `https://user-names.githubusercontent.com/{user_number_id}/{filename}`{: .filepath} 의 주소가 뜨게 된다. 
여기서 user_number_id는 항상 동일하기 때문에, 우리는 이 부분까지를 img_cdn으로 설정한다. 이후에 이미지를 넣을 땐 이렇게 복사 붙여넣기를 한 후 img path에 저 `/{filename}`{: .filepath}만을 작성하면 된다. 

그러면 아무 문제 없이 블로그에 내가 원하는 이미지들을 넣을 수 있게 된다. 역시 킹왕짱 깃헙 .. 사랑해요 🥹

## 기타 세팅들
- 우선, 나는 현재 덕질용 트위터 계정은 있으나 (ㅎㅎ) 개인용 트위터 계정은 없고 rss feed도 없기에 `_data/contact.yml`{: .filepath}에서 해당 부분도 주석처리들을 해주었다.

```yaml
- type: github
  icon: "fab fa-github"

# - type: twitter
#   icon: "fab fa-twitter"

- type: email
  icon: "fas fa-envelope"
  noblank: true # open link in current tab

# - type: rss
#   icon: "fas fa-rss"
#   noblank: true
# Uncomment and complete the url below to enable more contact options
```

- 또한, 아직은 아카이브할 것도 없기에 탭에서 아카이브도 없애주고 about을 위로 올려주었다. `_tabs/about.md`{: .filepath}에서 order를 3으로 수정하고 설명만 살짝 수정하였다. 


## Jekyll-compose plugin 
기본적으로 jekyll post들에서 지켜주어야하는 양식이 있다. 제목에 바로 `yyyy-mm-dd-title.md`{: filepath} 형식을 갖추어야 한다. 또한, 기본적인 **front matter**를 세팅하면 더 일관적인 포스트들을 작성할 수 있다. 

하지만 이걸 계속 기억하고 살기에는 나의 기억력이 좋지도 않을 뿐더러, 너무 반복적인 작업이다🥲 이를 손쉽게 해줄 수 있도록 도와주는 것이 바로 <span style="color: royalblue; font-weight: bold;">jekyll-compose</span> 플러그인이다. 정보는 [jekyll compose github](https://github.com/jekyll/jekyll-compose)에서 더 확인할 수 있다.

간단하게 설명하면, **명령어 하나로 기본적인 포맷을 맞춰 파일들을 생성해주는 플러그인**이다. 물론 포스트 뿐아니라 페이지 등도 가능하지만, 내 최우선 목표는 포스트 포맷화의 자동화다. 

### Jekyll-compose plugin 설치
우선 해당 plugin을 적용하기 위해 `Gemfile`{: .filepath}에 아래 내용을 추가해준다.

`gem 'jekyll-compose', group: [:jekyll_plugins]`

그 후 `bundle` 을 실행시켜 적용시켜준다.

### Jekyll-compose plugin 활용
그 후에 `bundle exec jekyll post "title"`을 하면 `yyyy-mm-dd-title.md`로 자동으로 포스트를 생성해주고, front matter 역시 기본적인 title과 date를 설정해준다.

그러나, 나는 category와 tags도 자동으로 front matter에 추가해주었으면 좋겠기에 `_config.yml`에 해당 부분을 추가해주었다.
```yaml
jekyll_compose:
  default_front_matter:
    posts:
      category:
      tags:
```

이렇게 하면 jekyll compose 플러그인을 활용하여 자동으로 post를 생성하게 되면 아래와 같이 기본 front matter가 설정한 파일이 생성된다.
![jekyll compose 플러그인을 통해 생성한 post front matter](/230946598-607bdab5-e79d-4a65-9ce8-494fc3a4b847.png)

이렇게 반복적이고 암기적인 작업을 한 번에 끝낼 수 있게 됐다 ! 


<br />
<div align="center" style="font-weight: bold;">
이렇게 기본적인 블로그 jekyll 세팅은 끝 🩵
</div>



