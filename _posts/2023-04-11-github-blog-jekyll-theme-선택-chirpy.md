---
layout: post
title: "[Github blog] jekyll theme 선택 - Chirpy"
date: 2023-04-11 00:34 +0900
subtitle: Jekyll theme 중 Chirpy 선택 및 이를 이용해 블로그 제작
category: [Web, blog]
tags: [github blog, blog, jekyll, chirpy]
---

## Jekyll theme 중 원하는 테마 고르기

Jekyll을 이용해 블로그를 만들어가는 사람이 많은 만큼, 이미 수많은 Jekyll blog theme들이 제작되어
무료 혹은 유료로 배포되고 있다. 그들 중 마음에 드는 것을 골라서 적용해보자 🫶

### Jekyll theme들을 모아볼 수 있는 사이트

Jekyll theme들은 많을 뿐만 아니라, 이들을 모아서 정리해놓은 사이트들도 있다. 많은 사이트들이 있으나 여기서는 두 개만 소개하자. (사실 나는 github에서 jekyll을 검색하고 fork 수를 보고 선택하긴 했다 😇)

1. [jekyllthemes.io](https://jekyllthemes.io/free)
2. [jekyll-themes.com](https://jekyll-themes.com/free)

나는 이 중에서 <span style="color: royalblue; font-weight: bold;">chirpy</span>을 골라서 적용하기로 했다. 

## Jekyll-theme-chirpy 적용

Jekyll theme들 중 chirpy를 선택해서 적용하기로 했다. 이제 이걸 어떻게 적용하는가 ?
바로 이 [Chirpy github](https://github.com/cotes2020/jekyll-theme-chirpy)을 참고하면 아주 손쉽게 적용할 수 있다. 그들의 깃헙 위키에서 Getting started를 클릭하면 무려 그들이 jekyll로 만든 포스트로 이동하게 된다. 

총 두 가지 방법이 있다.
1. Chirpy Starter를 이용하는 방법: upgrade가 쉽고 불필요한 프로젝트 파일들이 없다
2. Github fork를 이용하는 방법: 커스텀하기엔 쉬우나 업그레이드가 어렵다. 이들의 위키에서 이야기하기론, 'tweak'하거나 'contribute'하지 않을 것이면 비추천한다고 한다.

이럴 땐 말을 잘들어야 한다. 아직 더 하고 싶은 일들이 너무 많기에 jekyll에까지 기여하는 것은 너무 벅차다🥲.
그래서 [Chirpy Starter](https://github.com/cotes2020/chirpy-starter)를 이용해서 새 블로그 사이트를 만들어 보기로 한다. 여기서 설명대로 `Use this template` -> `Create a new repository` 를 선택해서 손쉽게 블로그를 만들었다 

## 적용한 chirpy blog 확인

`bundle`을 통해 dependencies들을 모두 설치해준 후 local 서버를 열어 본다. 아래 커맨드를 입력하면 localhost의 Port 4000번으로 블로그 서빙이 되게 된다. 다만, 파일 저장 후 새로고침을 해주어야 내용이 반영된다.
```shell
bundle exec jekyll s
```

## Blog deploy

기본적으로 Github은 jekyll에 대한 지원이 아주 뛰어나다. 그리고 대부분의 jekyll theme들은 아주 잘 작성이 되어 있어서, git에 푸쉬하는 것만으로도 자동으로 CD가 돌아가서 배포가 된다. 
github action으로 해당 내용은 `.github/workflows/pages-deploy.yml`{: .filepath}에서 확인할 수 있는데, `main` 혹은 `master` 브랜치에 푸쉬하게 되면 자동으로 Build 후 Deploy하는 workflow가 실행된다.

이렇게 기본적인 세팅은 끝! 
다음 포스팅에서는 이렇게 만든 블로그의 기본 configuration들과 추가한 이런저런 것들을 소개해보고자 한다.

<br />
<div align="center" style="font-weight: bold;">
이렇게 chirpy theme을 적용한 jekyll 블로그 사이트 생성 완료 🩵
</div>




