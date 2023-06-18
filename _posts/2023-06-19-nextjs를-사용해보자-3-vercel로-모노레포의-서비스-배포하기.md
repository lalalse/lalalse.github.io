---
layout: post
title: nextjs를 사용해보자 - 3. vercel로 모노레포의 서비스 배포하기
date: 2023-06-19 01:16 +0900
subtitle:  nextjs를 사용해보기 위한 탐험기. 3) vercel로 모노레포 서비스 배포
category: [Web, frontend]
tags: [frontend, nextjs, vercel, turborepo, monorepo, deploy]
---

처음부터 완벽한 CI/CD pipeline을 익히면 좋겠지만, 우선은 이렇게 세팅한 모노레포의 서비스를 간단하게 deploy하는 방법을 알아보도록 하자. 배포하는 과정을 좀 잘 익혀놓을걸 후회했지만 .. 따라가보도록 하자


### 1. vercel에서 project 연결하기
monorepo에서 각 서비스를 배포할 것이기에 프로젝트 이름은 서비스 이름으로 한다.
그 후, 모노레포인 github repo를 연동시켜준다.

### 2. root directory 설정
root directory를 `apps/{프로젝트 이름}`으로 설정한다.

### 3. build & development settings
이 부분이 가장 중요하다 ! 필자는 크게 두 가지 command를 수정했다.

- build command
- install command

- build command
  기본적인 next의 build를 적용하면 안되고, monorepo라는 점을 상기해야한다.
  ```
  cd ../.. && npx turbo run build --scope={프로젝트 이름} --include-dependencies --no-deps
  ```

  가장 윗단인 전체 모노레포로 이동한 후 (`cd ../..`), 
  프로젝트에 대해 build해야 한다 (`npx turbo run build --scope={프로젝트 이름} --include-dependencies --no-deps`)
  이 때, `--include-dependencies --no-deps`를 함꼐 사용해 해당 스크립트에 필요한 의존성을 함께 실행해주어야 한다.

### 4. 끝
이제 github에도 연동시켜놓았고 기본적인 CD는 진행된다 !
main branch에 푸쉬하면 자동으로 deploy가 진행된다.

만약 프로젝트 레포가 많아지면, git diff 등을 사용해서 바뀐 레포에 대해서만 재배포하는 github action을 실행해야겠지 !
우선은 test 등도 필요 없는 정말 비상업용, 선물용 프로젝트 기에 test를 포함한 CI는 정확한 스펙을 생각해보고 도입하는 걸로!

<br />
<div align="center" style="font-weight: bold;">
이렇게 vercel로 모노레포의 프로젝트 배포 기본 습득 완료 🩵
</div>



