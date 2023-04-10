---
layout: post
title: "[Github blog] 기본 theme 세팅을 덮어써서 커스텀하는 방법"
date: 2023-04-11 03:22 +0900
subtitle: Post 미리보기에 내용 대신 부제를 보이게 하고, Post에 부제를 쓰자 ! 
category: [Web, blog]
tags: [github blog, blog, jekyll, chirpy, html, customization]
---


## Motivation
이런저런 블로그 포스팅을 하다가 보니, 나는 이렇게 내용 앞부분에는 이 글을 쓰게 된 이유에 대해 사설 느낌으로 주저리주저리 쓰는 느낌이 강하게 들었다.

그런데 Chirpy의 기본 세팅에서는 post 미리보기에 항상 제목과 내용 일부가 보인다는 단점이 있었다🥲. 뭔가 미리보기에 딱 핵심만 보였으면 좋겠는 마음이 들어서 이 부분을 1차적으로 커스텀해보기로 했다.


## Customization 방법
Chirpy starter로 블로그를 만들 경우, html 파일들이 들어있지 않다. 이를 이용해 레포를 만들 경우, 자동으로 [fork된 chirpy](https://github.com/lalalse/jekyll-theme-chirpy)가 생성된다. 
그리고 `_config.yml`{: .filepath}에서 theme을 통해 해당 파일을 이용해서 작성되게 된다.

이 때 어떻게 **커스텀**하는가? 바로 원하는 파일을 만들어서 <span style="color: red; font-weight: bold">overwrite</span>하면 된다.

### Customization 하고 싶은 부분
그렇다면, 우선 어떻게 커스텀할 것인가를 정해야한다. 바로 <span style="color: royalblue; font-weight: bold">부제(subtitle)</span>을 사용하는 것이다.
내용 미리보기의 영역 대신 부제를 사용하면 해당 글의 핵심을 좀 더 담을 수 있지 않을까?


## Post에 부제를 적용하는 방법

### 1. post들에 subtitle를 추가하자
**우선 post들에게 공통적으로 subtitle들을 필수 변수로 갖게 하자.**
이를 위해선 이전에 작성했던 게시글과 같이 `_config.yml`{: .filepath} 의 jekyll_compose default front_matter의 posts부분에 subtitle을 추가해준다.
이렇게 되면 기본적으로 post를 만들 때 subtitle가 추가되어 생성된다.

이렇게 front matter에 작성해주면 post에 subtitle가 생기게 된다. 
그 후에 원래 내용의 미리보기가 떴던 부분에 이 post의 subtitle을 대신 작성하면 된다.


### 2. home의 post 미리보기를 변경하자
home에서 각 post card의 layout을 수정하자. 
기존의 `_layouts/home.html`{: .filepath}을 복사한 후에 line 52의 아래 부분을 수정하면 된다.

```liquid
{% raw %} 
{% include no-linenos.html content=post.content %}
{% endraw %}
```
{: .nolineo}

이 부분이 post card에 content 미리보기를 할 수 있게끔 해주는 부분이다. truncate 200을 통해 일부만 보여줄 수 있도록 작성되어있다. 이를 아래와 같이 수정한다.

```liquid
{% raw %}
{% include no-linenos.html content=post.subtitle %}
{% endraw %}
```
{: .nolineo}

그 결과, 아래와 같이 홈 화면이 깔끔해졌다 ! 
![홈 화면 변경 결과](/230970253-b9d213e7-5aa1-4b67-a5bd-3596be4f91dc.png)

### 3. post에서 title 아래에 subtitle이 뜨게 하자
subtitle을 만들었는데 정작 post에서 안 보이면 웃기지 않나...? 해서 post에도 제목 아래에 subtitle을 넣어주기로 했다.
기존의 `_layouts/post.html`{: .filepath}를 복사한 후에 title 내용을 담은 line 12 아래에 이와 같은 코드를 추가해주었다.
```html
<p class="post-meta subtitle">{{ page.subtitle }}</p>
````
이렇게 하면 title 밑에 subtitle이 p tag로 생성되게 된다. 여기서 class name을 부여해줌으로써 이 부분 스타일 수정이 쉽게 가능하게 했다.

`assets/css/style.scss`{: .filepath}를 만들었고 아래와 같은 내용을 추가해주었다.
이 때 이 subtitle 뿐 아니라 heading들의 css 스타일도 약간 수정해주었다.
```
{% raw %}
---
---

/*
  If the number of TAB files has changed, the following variable is required.
  And it must be defined before `@import`.
*/

$tab-count: {{ site.tabs | size | plus: 1 }}; // plus 1 for home tab

@import "{{ site.theme }}";

/* append your custom style below */
h1 {
  font-weight: 700;
}

.subtitle {
  font-size: 1rem;
  font-style: italic;
}

h2 {
  font-weight: 700;
}

h3 {
  font-weight: 700;
}

h4 {
  font-weight: 700;
}
{% endraw %}
```


그 결과, 아래와 같이 post 화면에 subtitle이 잘 뜨게 되었다 ! 
![post 화면 변경 결과](/230970490-1175ed00-74d6-4232-9b6d-80ade4a7ae47.png)

### 4. 관련된 글에서도 subtitle이 뜨게 하자 
거의 똑같은 로직이다. `_includes/related-posts.html`{: .filepath}에서 해당되는 부분을 수정해주면 된다. 여기서는 line 93을 똑같이 수정해주면 된다.
```liquid
{% raw %}
{% include no-linenos.html content=post.subtitle %}
{% endraw %}
```
{: .nolineo}

그 결과, 관련된 글 카드에서도 무사히 subtitle이 잘 뜨게 되었다 !
![관련된 글 화면 변경 결과](/230971021-4912e0c9-5167-4557-b868-56e4621fc743.png)

### Summary
위에서 여러 개에 나누어 작성했으나, 결국 가장 중요한 부분은 해당되는 파일을 <span style="color: red; font-weight: bold">overwrite</span>해주면 된다. 기본 html 파일의 구조는 파악이 가능하니까 😉
그렇다면 해당되는 파일을 어떻게 찾았느냐 ? 
이미 chirpy 폴더 구조가 굉장이 잘 되어있는 편이긴 하지만, 처음에 일일이 찾기엔 복잡한 감이 있다. 

그럴 땐 **브라우저의 검사 도구**를 이용해 바꾸고 싶은 부분의 **class 이름** 등을 찾는다.
그 후, **github 레포 내 검색**에서 해당 class name을 검색 후 관련된 파일들을 확인하면 좀 더 손쉽게 찾을 수 있었다. 더 좋은 방법이 있을 것 같긴 하지만, 이 정도로도 충분히 빠르게 커스텀할 수 있었다.
이 팁이 처음 커스텀을 하고자 하시는 분들께 도움이 되길 바란다...🥹

<br />
<div align="center" style="font-weight: bold;">
이렇게 부제를 적용하는 커스텀 및 커스텀 방법 체득 완료 🩵
</div>





