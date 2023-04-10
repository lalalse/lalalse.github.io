---
layout: post
title: "[Github blog] jekyll liquid escape를 해보자"
date: 2023-04-11 04:25 +0900
subtitle: 자동으로 Liquid 처리되는 부분을 어떻게 피할까?
category: [Web, blog]
tags: [github blog, blog, jekyll, liquid, escape]
---



> {{"{% raw"}} %} 와  {{"{% endraw"}} %}를 사용하자 
{: .prompt-tip }

Jekyll은 [공식 문서](https://jekyllrb.com/docs/liquid/)에도 나와있듯이 **Liquid** template를 이용한다. 

Liquid의 경우엔 주로 
`{% raw %}{{ variable }}{% endraw %}`
또는
`{% raw %}{% if statement %}{% endraw %}`를 통해 템플릿화한다.

다만, 여기서 문제가 생겼다. 난 이 블로그에 Jekyll 다루는 방법에 대해서 포스팅을 하고 있다.
그렇다면 이 Liquid 문법을 어떤 식으로 썼는지를 써야 한다.
그러나 그냥 markdown에 작성하면 해당 부분을 Liquid로 인식해서 자동으로 포맷팅이 되거나 인식이 되지 않는다.

이 문제를 [이전 글](https://lalalse.github.io/posts/github-blog-%EA%B8%B0%EB%B3%B8-theme-%EC%84%B8%ED%8C%85%EC%9D%84-%EB%8D%AE%EC%96%B4%EC%8D%A8%EC%84%9C-%EC%BB%A4%EC%8A%A4%ED%85%80%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95/)을 작성하면서 너무 크게 겪었다. 

```liquid
{% raw %}
{% include no-linenos.html content=post.subtitle %}
{% endraw %}
```
이 부분을 markdown에 담고 싶었는데, 계속해서 그대로 입력하면
```liquid
{% include no-linenos.html content=post.subtitle %}
```
이렇게 아무것도 뜨지 않는 것이다🥲 내가 뭘 잘못했나 싶고 ...

그렇게 찾아본 결과 liquid 문법에서는 "해당 부분은 raw text이며 liquid 문법이 아니다"라고 어찌보면 **escape**하는 방법이 있었다.

바로 아래와 같이 작성하면 된다 
```
{{"{% raw"}} %} {{"{{ example"}} }} {{"{% endraw"}} %}
{{"{% raw"}} %} {{"{% example"}} %} {{"{% endraw"}} %}
```

<br />
<div align="center" style="font-weight: bold;">
이렇게 무사히 liquid 문법도 블로그에 포스팅할 수 있게 되었다 🩵
</div>



