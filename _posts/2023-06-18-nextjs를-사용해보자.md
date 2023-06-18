---
layout: post
title: nextjs를 사용해보자 - 1. turborepo를 이용한 모노레포 세팅
date: 2023-06-18 21:45 +0900
subtitle: nextjs를 사용해보기 위한 탐험기. 1) 기본 모노레포 세팅 
category: [Web, frontend]
tags: [frontend, nextjs, vercel, turborepo, monorepo]
---

### tmi

두 달동안 개발은 생각도 못하고 덕질에 몰두해 살았다 (..) <br />
이번에 만들어서 간편하게 배포해보고 싶은 사이트가 있었는데, <br />
vercel - nextjs 조합을 이용하면 손쉽고 저렴하게 배포가 가능할 듯 해서, nextjs라는 프레임워크를 처음으로 사용해보기로 한다. <br />
이 사이트와 같은 형식이 앞으로도 계속 증식할 수 있을 것 같아, monorepo를 적용해보자.

vercel에서 nextjs와 turborepo를 공식적으로 서비스하기에,
다양한 monorepo들이 있지만 궁합이 가장 좋을 것 같아 nextjs + turborepo + (vercel) 을 이용하여 작업해보는 여정을 다뤄보고자 한다.

tmi지만, 사실 이정도 개발을 하지 않으면 정말 덕질에만 몰두하고 살아서 뇌가 굳을 것 같아, 덕질과 개발을 융합해보기로 결정했다.
공개할 수 없는 정보가 많을 것 같아 우선적으로 대략적인 방법이나 troubleshooting 위주로 기록하는 것을 목표로 한다.

그래서 앞으로 당분간 간단한 페이지가 될 테지만, **nextjs + turborepo + vercel** 사이트 배포를 목표로 개발을 한다.


### turborepo 세팅 

간단한 기본 세팅 방법은 다음과 같다.

```shell
npx create-turbo@latest
```

위 명령어를 치면 간편하게 커맨드라인을 통해 turborepo가 적용된 환경을 구축할 수 있다.
패키지 매니저는 pnpm을 사용하도록 한다.

그 후에 보면 이런 식의 폴더 구조로 만들어진다. 
![turbo 폴더 구조](https://github.com/lalalse/lalalse.github.io/assets/129953891/53e183ed-7147-4e42-90ab-eabe137c10f7)

우선 대략적인 폴더 구조를 파악해보면,

1. apps: 보통 실제로 원하는 페이지들의 프로젝트 폴더 
- 기본적으로는 docs, web으로 되어있고 해당 부분은 변경할 예정!

2. node_modules: 모노레포로 관리하기에 이들을 관리하는 전체 node_modules 폴더

3. packages: 모노레포 전체에서 쓰이는 vozlwlemf wjdfl
- eslint-config-custom: eslint 공통적으로 적용할 수 있게 configuration 세팅할 수 있도록
- tsconfig: tsconfig 
- ui: 모노레포에서는 주로 UI component를 공유해서 많이 사용하기에 이를 위한 ui package

4. 그 외
- eslintrc, package.json ,. ... 


한 번 두드려가보면서 알아보자


### 사이트 구동

간단한다. 전체 package.json에 있는 대로 ```pnpm run dev``` 실행하면 3000번 포트에 web, 3001번 포트에 docs가 구동된다.

이제 우선 원하는 사이트 하나 구축이 목표기에, apps에 원하는 프로젝트를 만들어서 진행하도록 할 예정 ! <br />
하지만 우리 모두 알듯이 .. 이제 시작이다 .. 이전 회사에서도 거의 부딪혀가면서 진행해보았기 때문에 이번에도 그럴 예정 ! 
아직은 꽃밭이다 ㅎ_ㅎ


<br />
<div align="center" style="font-weight: bold;">
이렇게 초간단 turborepo를 활용한 모노레포 세팅 완료 🩵
</div>


