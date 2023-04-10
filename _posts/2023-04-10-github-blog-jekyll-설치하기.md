---
layout: post
title: "[Github blog] Jekyll 설치하기"
date: 2023-04-10 13:28 +0900
subtitle: rbenv를 이용한 ruby 관리 및 jekyll 설치
category: [Web, blog]
tags: [github blog, blog, jekyll, ruby, rbenv]
---

본 포스팅은 jekyll 설치 이후에 작성되었므로, 처음부터 설치할 경우 사진 등이 다르게 보일 수 있습니다. 

## Jekyll 설치를 위한 ruby setting

Jekyll의 경우 ruby를 기반으로 한 프레임워크로, ruby가 설치되어 있어야 한다.  
mac에서는 ruby가 기본적으로 설치되어 있으나, [Jekyll 홈페이지](https://jekyllrb.com/)의 설명대로 할 경우, 오류가 발생한다. 

mac의 ruby의 경우 system ruby를 사용하고 있기에, sudo를 통해 root 권한이라면 설치가 가능하나,
보안 상의 이유로 권장되지 않는 설치법이라고 한다. [참고 블로그 글](https://til.younho9.dev/docs/frontend/jekyll/jekyll-github-page%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%B4-%EA%B0%9C%EC%9D%B8%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0/)

<span style="color: royalblue; font-weight: bold;">rbenv</span> 이라는 ruby version
관리자를 설치하고, 이를 통해 system ruby가 아닌 별도 버전의 ruby 환경을 만들고 관리하는 것이 좋다.

### rbenv 설치

`brew install rbenv`를 통해 rbenv를 설치할 수 있다.
그 후 `rbenv versions`를 통해 현재 rbenvd에서 관리하고 있는 버전들과 현재 세팅되어있는 ruby version을 확인이 가능하다.

우선, jekyll을 위해 사용할 ruby 환경을 만들기 위해 
`rbenv install -l`을 통해 가능한 버전 목록을 볼 수 있고 그 중 하나를 선택해서 설치하면 된다.
나는 그 중 **3.0.6** 버전을 선택해 `rbenv install 3.0.6`를 롱해 설치해주었다.
설치 후 rbenv로 글로벌 버전을 설치한 루비 버전으로 변경한다. (system -> 새로 설치한 ruby)


![ruby version 변경 결과](/230827623-51a3352b-26a9-4097-9e2c-0be3867d291a.png)

이렇게 완료되면 정상적으로 system ruby가 아닌 rbenv를 통해 별도 설치된 ruby 환경으로 세팅이 되었다.

*다만, 이 과정에서 놓쳤던 부분이 있었다. 바로 되면 배우는게 없지 ...* <br /> 
블로그를 그대로 따라가다 보니 rbenv 설치를 그냥 대강 넘겨버린 것🥲 꼭 무엇 하나를 설치하더라도 공식 문서를 참고하는 습관을 들이자.

처음 설치 시에 `rbenv init`을 통해 나온 rbenv를 쉘에 적용하기 위한 안내 사항이 나오는데 이를 넘겨버렸다.
`eval "$(rbenv init -)"`를 shell 세팅에 추가해주어야 한다. 
우리는 [m2 터미널 세팅](https://lalalse.github.io/posts/m2-%ED%84%B0%EB%AF%B8%EB%84%90-%EC%84%B8%ED%8C%85%ED%95%98%EA%B8%B0-iterm2-oh-my-zsh/)에서 세팅했듯이 zsh를 사용하기 떄문에,
 `~/.zshrc`{: .filepath} 에 `eval "$(rbenv init -)"` 내용을 추가해주었다. 

이렇게 되면 무사히 jekyll을 설치하기 위한 ruby setting이 끝났다 ! 

## Jekyll 설치

이제 문제없이 jekyll과 bundler를 설치할 수 있다.
Ruby Gem을 이용해 jekyll 홈페이지에 명시되어있는 방법을 따라 설치한다.

`gem install jekyll bundler` 

<br />
<br />
<div align="center" style="font-weight: bold;">
이렇게 rbenv를 통한 ruby 세팅과 jekyll 설치 완료 🩵
</div>


