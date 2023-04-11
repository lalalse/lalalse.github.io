---
layout: post
title: "[Frontend 세팅] rush를 이용한 Monorepo 관리"
date: 2023-04-12 01:13 +0900
subtitle: 하나의 동일한 성격의 서비스들을 한 곳에 쉽게 관리하기 위한 모노레포 선택 및 rush 적용
category: [Web, frontend]
tags: [frontend, rush, npm, pnpm, monorepo]
---

이전 회사에서 프론트엔드 작업을 하면서, monorepo를 적용했던 경험이 있다. 두 개 이상의 프로젝트를 하나의 깃 레포에 저장하는 소프트웨어 개발 전략이다.
하나의 공통된 Git 레포에서 여러 패키지들을 이용하고 버전 관리하기 쉬운 장점이 있었고,
여러 프로덕트를 개발할 때 각 프로젝트별 코드 컨벤션 통일이나 이런 측면에서 장점이 있었다. 
또한 한 번 Lint 또는 Test 등을 세팅해놓으면 하나의 깃 레포로 관리되니까 세팅에 드는 비용이 적어졌었다. 

물론, 굉장히 다른 성격의 프로젝트들은 멀티 레포로 관리하는 것이 나을 수도 있다.
우선 이번에 사이드 프로젝트들을 진행함에 있어서 성격이 비슷하거나 목적이 유사한 경우 하나로 묶어서 모노레포 전략을 사용해보기로 했다.
(우선, 사이드 프로젝트의 일반 사이트와 어드민 사이트를 한 레포에 넣어서 쓰도록 해볼 것 같다)

## Rush 

그 중 Rush라는 마이크로소프트사에서 만든 모노레포 프레임워크를 적용하기로 했다. 우선, 이전에 사용해봐서 익숙하기도 했고 여러 장점들이 있었다. 
[Rush 모노레포 도입기](https://medium.com/mildang/rush%EB%A1%9C-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C-%EB%AA%A8%EB%85%B8%EB%A0%88%ED%8F%AC-%EB%8F%84%EC%9E%85%EA%B8%B0-5da0c5bc9b30) 
해당 블로그 글을 많이 참고하면서 정했던 기억이 있다.

우선, 내게 가장 큰 장점으로 다가온 것은 **pnpm** 패키지 매니저를 사용하여 단일 루트에 설치한 후 심링크를 통해 연결하기에 phantom dependency가 없고, 똑같은 패키지를 여러 번 설치하지 않아도 된다라는 장점이었다. 

그 외에 빠른 빌드, 하위 집합 및 incremental 빌드, cyclic dependencies, 대량 퍼블리싱 등 다양한 장점이 있다고 하지만 이런 것들은 체험해봐가면서 꺠달아야 하는 것 같다. rush에 좀 더 익숙해지면서 장점을 파악해보는 것으로 ..! 

### Rush 설치

Rush 설치는 간단하다. node만 깔려있다면, 아래 명령어를 통해 손쉽게 설치 가능하다.
```shell
npm install -g @microsoft/rush
```

### Rush 적용

원하는 repo로 들어간 후 `rush init`을 통해 rush 초기 세팅을 해주면 된다.
그 결과, 해당 레포에 이런 식으로 rush의 기본 세팅이 들어가게 된다.

![rush 초기 세팅 결과](/231231362-453c9aad-70ee-483a-9b4b-27ddcb40b49d.png)

### Rush 사용시 유의점
Rush는 기본적으로 모노레포의 패키지 매니저로서의 역할을 수행한다. 그렇기에 npm이나 pnpm 같은 패키지 매니저 사용을 지양해야 한다. 이들이 중복되어 수행될 경우 귀찮은 일들이 생겨버린다. 
1. `rush update` 생활화 
  - `package.json`{: .filepath} 관련 변경 사항이 있을 경우 한 번씩 꼭 update해주는 것이 좋다. 
  - 이 외에 common 폴더의 사항들을 수정했을 때도 해당된다. 예를 들어 `common/git-hooks`{: .filepath}에서 수정사항이 생긴다고 바로 업데이트되는 것이 아니라 `rush update`를 수행해야 내 `.git`{: .filepath}에 반영이 되고 의도한 대로 작동한다. 
  - 유의해야할 점: CI에서는 `rush update`가 아닌 `rush install`을 통해 진행되고 `rush install`의 경우는 다른 파일들을 업데이트하지 않아 빌드에 실패할 수 있다. 즉, `rush update`를 생활화하고 잘 커밋해서 푸쉬하도록 하자. 
  - rush update가 수행하는 작업은 이와 같다.
      1. `common/config`{: .filepath}의 다양한 정책들을 확인하고 적용한다.
      2. 모든 프로젝트의 `package.json`{: .filepath}을 해당 repo의 공통된 shrinkwrap 파일과 비교하여 확인 후 유효한지 확인한다.
      3. outdate된 경우 shrinkwrap 파일을 업데이트한다. 
      4. 이렇게 패키지 매니저는 모든 dependency들을 `common/temp/node_modules`{: .filepath}에 설치한다.
      5. 각 프로젝트 별 `node_modules`{: .filepath}에 심링크를 이용하여 사용하는 패키지들을 구성한다.


2. `rushx`
  - 한 레포에서 여러 프로젝트들을 관리하기 때문에, 각 프로젝트 별로도 `npm start`와 같은 역할 등을 할 수 있어야 한다. 이를 위한 것이 바로 `rushx`이다. 해당 사용법은 천천히 알아가보도록 하자.


3. `rush add`
  - 프로젝트에 패키지를 추가하는 방법이다. 이 때 주의할 점은, rush가 기본적으로 패키지 매니저의 역할을 함을 잊지 말자. **npm** 또는 **pnpm**과 같은 다른 패키지 매니저들과 혼용해서 사용하면 복잡해진다. 
  **rush에서 패키지를 수정할 땐 꼭 rush 커맨드를 사용하도록 하자**


4. `rush remove`
  - 프로젝트에서 패키지를 삭제하기 위한 방법이다. 이 역시 위의 `rush add`와 유사하다.

  
기본적인 사용법은 이와 같고, 세부적인 내용이나 사용 방법은 다음 포스팅들에서 직접 프로젝트들을 추가하면서 써보자

<br />
<div align="center" style="font-weight: bold;">
이렇게 원하는 웹레포(덕질 레포가 될 예정)에 모노레포 rush도 적용 완료 🩵
</div>


