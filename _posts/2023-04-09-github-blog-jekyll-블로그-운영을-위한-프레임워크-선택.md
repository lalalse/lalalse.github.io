---
layout: post
title: "[Github blog] Jekyll - 블로그 운영을 위한 프레임워크 선택"
date: 2023-04-09 14:44 +0900
subtitle: Github blog 운영을 위해 Jekyll을 선택한 이유 
category: [Web, blog]
tags: [github blog, blog, jekyll, static web]
---


## 사설
이전 회사에서 개발을 시작하면서 개발에 대한 시작과 동시에 task 처리에 급급하다 보니, 
어떠한 문제를 해결함에 있어서 그 과정을 제대로 기록하지 못했다는 점이 아쉬움으로 항상 남아있었다.  <br />

그리고 이렇게 하고 싶은 걸 할 수 있는 기간이 찾아오면서, 
이런저런 하고 싶은 개발도 하고 그 과정을 기록으로 남겨보면 좋지 않을까 해서 
"내 블로그"를 만들어보면 좋을 것 같다는 생각을 강렬하게 했다.
<br />

그러면서 찾아본 것이 **[tistory, velog, 자체 개발 블로그]** 였다. <br />
세 개의 장단점은 굉장히 여러 게시글들에 소개되어있지만, 
내가 자체 개발 블로그를 선택한 이유 중 가장 큰 것은 'fancy'해보인다는 것이었다. 
초기의 세팅에는 다른 두 개보다 좀 더 걸릴 수 있지만, 일단 시작하면 멋져 보이기도 하고 
익숙해지면 자유자재로 커스텀하기도 쉽지 않은가? 하는 마음에 <span style="color: red; font-weight: bold">자체 개발 블로그</span>를 선택했다. 
<br />

자체 개발 블로그를 호스팅을 통해 별도의 웹사이트로 만들 수 있었으나, 
개발자에겐 킹왕짱 Github이 심지어 free plan 사용자에게도 **github page**를 통해 
웹사이트를 호스팅할 수 있게 해준다. 이를 선택하지 않을 이유는 없었다. 
<br />

## 개요

Github blog를 선택하면서 이용하기로 한 프레임워크는 **Jekyll** 이다. <br />
Github에서 Jekyll CMS를 내장하고 있기도 하고, 프레임워크 특징으로 별도의 데이터베이스가 필요 없기에 서버를 갖추지 않고 무료로도 충분히 가볍게 사용할 수 있다. 또한, 이미 많이 사용되고 있는 프레임워크인 만큼 다양한 테마 선택이 가능했다.

### Jekyll 이란 ? 
<span style="color: red; font-weight: bold;">Jekyll</span>은 Ruby 언어를 통해 개발된 프레임워크이다. 그들이 내세우는 캐치프레이즈는 다음과 같다.
> Transform your plain text into static websites and blogs.

즉, 손쉽게 텍스트 형태를 정적 웹사이트와 블로그에 특화되어 보여주는 것에 목표를 둔 프레임워크이다.
그들이 [홈페이지](https://jekyllrb.com/) 에서 내세우는 특징은 크게 세 가지이다.
1. <span style="color: royalblue; font-weight: bold;">Simple</span> : 데이터베이스가 필요 없고, 급변적인 업데이트가 없이 오로지 컨텐츠로만 이루어진다.
2. <span style="color: royalblue; font-weight: bold;">Static</span> :
Markdown, Liquid, HTML & CSS 베이스로 이루어진 정적 웹사이트의다.
3. <span style="color: royalblue; font-weight: bold;">Blog-aware</span>:
링크, 카테고리, 페이지, 포스트, 커스텀 레이아웃 등 블로그에 안성맞춤이다.

### 정적 웹과 동적 웹

그렇다면 정적(Static) 웹과 동적(Dynamic) 웹의 차이점은 무엇인가?
<br />

**정적 웹** 
- 요청에 따라 미리 저장된 페이지를 응답 
- 웹 서버가 필요하지 않다. 백엔드 코드가 없어 제작이 간편하다.
- 속도가 빠르다. 복잡한 로직이 필요 없는 소규모 사이트에 적합하다.
<br />

**동적 웹**
- 요청에 따라 서버가 데이터를 전달 / 데이터베이스 등이 연동 가능
- 동일한 페이지도 요청에 따라 다양한 내용이 응답 가능하다.
- 속도가 서버의 사양에 따라 차이가 크나, 로직이 복잡한 사이트에 적합함.
- 대부분의 웹 사이트에 해당한다. 
<br />

개인 소규모 블로그 운영에는 데이터베이스 운영도 필요하지 않고, 사용자의 행동이 데이터베이스 등에 반영될 필요도 없기에 정적 웹만으로도 충분하다. 


### 그래서 Jekyll ! 

Jekyll은 이러한 특성을 반영해 사용자가 작성한 코드를 하나의 웹 프로젝트 형태로 빌드한다. 
Jekyll은 백엔드 코드에 대한 부담감이 없기에 간편하게 작성이 가능하다.

그런 만큼, 이 Jekyll은 블로그에 대한 모든 것이 **작성자 자신**에게 있다.
HTML, CSS에도 익숙해지는 겸 개발자의 Text인 markdown 문법에도 익숙해지고자 하는
나에게 너무 시작하기 적합한 프레임워크였다. 
아직 변방의 블로그이기에 댓글 등이 필요하지 않고 나의 연습 및 기록용이기에 이를 선택한 측면도 있다. 

*언뜻 찾아봤을 땐, jekyll 기반 웹사이트에도 댓글 기능을 추가하는 방법이 있다고 했으나 이건 필요할 때 적용하고 기록하면 되겠지 😇*


<p style="color: green; font-weight: bold;">Jekyll 추천 대상</p>
- 자신의 입맛에 맞게 블로그를 커스텀해가고 싶은 사람
- HTML, CSS 등 기본적인 웹 지식이 있는 사람 혹은 그에 익숙해지고 싶은 사람
- 블로그를 자체적으로 개발한다라는 fancy한 느낌에 끌리는 사람

*(적어보니 순전히 내 설명이다)*

<p style="color: red; font-weight: bold;">Jekyll 비추천 대상</p>
- 복잡한 것은 싫다. 안정적이고 심플한 것을 원한다.
- 기본적으로 플랫폼에서 제공되는 기능들만으로도 충분한 사람

*(사실 회사에 다닐 때 블로그를 작성해보자했다면 jekyll이 아닌 velog를 선택했을 것 같다)*


<br />
<br />

<div align="center" style="font-weight: bold;">
그래서 이 Jekyll 프레임워크 + github page를 이용해서 블로그를 운영해보기로 결정했다🩵
</div>



