---
layout: post
title: nextjs를 사용해보자 - 2. eslint configuration 세팅
date: 2023-06-18 22:47 +0900
subtitle: nextjs를 사용해보기 위한 탐험기. 1) 기본 모노레포 세팅 
category: [Web, frontend]
tags: [frontend, nextjs, vercel, turborepo, monorepo, eslint]
---

프론트엔드 작업을 시작하기 전에 기본적인 코드 포맷은 제한해두는 편이다.
물론 이런 것 없이도 코드가 통일성이 있고 간결하게 작성되면 좋겠지만, 그것은 정말 천재 아닌 이상 힘들다고 본다.
어제의 나와 오늘의 나는 같을 수 없기에 >..< <br />
그렇기에 코드 스타일을 강제할 수 있는 세팅을 웬만하면 초반에 꼭 해두는 편이다.
그 후에, 보통은 팀원들과 상의하여 너무 strict한 룰은 빼거나 일부 룰은 추가하는 편이다.

그러나 이번엔 우선 나 혼자 하는 것이기에, 기본 세팅인 airbnb를 먼저 적용하고 나머지를 차차 변경해가기로 !


### eslint-config-custom 적용 방법

turborepo에서는 손쉽게 전체 app들에 적용할 수 있도록 packages에 eslint-config-custom을 작성해두었다.
여기의 index.js를 변경하고 추후에 **app**들의 ```package.json``` , ```.eslintrc.js```에서 적용할 수 있다.


- package.json

eslint는 개발 시에 적용되는 시스템이기에 dependencies가 아닌 devDependencies에 적용해주면 된다.
```json
"devDependencies": {
  ...
  "eslint-config-custom": "workspace:*", 
  ...
}
```
기본적으로 packages에 작성된 모듈들을 import하기 위해선 `workspace:*`를 사용하면 된다.


-  .eslintrc.js

```js
module.exports = {
  root: true,
  extends: ["custom"],
};
```
eslint-config-* 패키지 이름을 사용하기 위해선 *만 사용하면 된다. 그렇기에 기본적으로 여기서 custom을 사용하고,
추후에 서비스 단에만 적용해야할 더 추가하거나 꺼야 할 것이 있으면 이 app단의 eslintrc 파일을 변경해주면 된다. 


### eslint 적용하기
우선 `packages/eslint-config-custom`으로 가서  `eslint-config-airbnb` 패키지를 설치해준다.
그 후 `index.js`에서 airbnb 세팅을 적용해준다.
```
extends:  ["next", "turbo", "prettier", "airbnb"],
```

우리는 nextjs를 사용할 것이기에, nextjs에선 기본적으로 React를 import한다.
그렇기에 import하는 것을 강제하는 rule을 꺼준다.
또한, .tsx, .ts파일에서 jsx 문법을 쓰고 싶기에 이 부분도 추가해둔다.

```
rules: { 
  "react/react-in-jsx-scope": 0,
  "react/jsx-filename-extension": [1, { "extensions": [".ts", ".tsx"] }]
}
```

그 후에 rules에 이런저런 세팅을 더 추가해두었다.
```
  "import/extensions": 0,
  "import/prefer-default-export": 0,
  semi: ["error", "never"],
```

또한 parser babel option에 React를 자동으로 인식시켜주는 부분을 추가해두었다.
```
parserOptions: {
  babelOptions: {
    presets: [[require.resolve("next/babel"), { "preset-react": { "runtime": "automatic" } }]],
  },
}
```

### eslint auto fix on save 적용

이걸 적용시키느라 정말 많이 서치했다 🫠 당연히 format on save를 적용하면 될 줄 알았지만 전혀 되지 않았음.

아래와 같은 기본 `settins.json` 을 세팅했는데 저장했는데 고쳐지지가 않는 것이다. <br />
그런데 이상하게 `pnpm lint --fix`하면 고쳐짐 😮

```json
{
  "eslint.workingDirectories": [
    {
      "mode": "auto"
    }
  ],
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "html",
    "typescriptreact"
  ],
}
```

그래서 eslint debug console을 살펴보았다.
![eslint debug 결과](https://github.com/lalalse/lalalse.github.io/assets/129953891/836a55bf-8459-4423-9a87-e39d71ca013b)

`next/babel`을 인식하지 못하는 것이다. 아 ! <br />
그래서 `packages/eslint-config-custom`에
`pnpm install next -D`를 통해 next를 devDependency에 추가해주었더니 되었다 😇

이제 eslint formatOnSave도 잘 작동함 !!

이제 끝없이 사용해보며 eslint 세팅을 바꾸는 과정 역시 남았지만, (세팅만 잘해두면 정말 좋다)<br />
그래도 turborepo + nextjs 조합에 eslint 적용하는 것까지 진행했다 굿 


<br />
<div align="center" style="font-weight: bold;">
이렇게 레포에 eslint 기본 세팅 완료 🩵
</div>

