---
layout: post
title: "[Python] 파이썬에 venv로 가상환경을 설정해보자"
date: 2023-04-16 22:36 +0900
subtitle: 파이썬 venv를 통해 가상환경을 만들고 VS code 및 jupyter lab에서 설정하기
category: [Etc., setting]
tags: [python, venv, visual studio code, jupyter]
---

python을 사용할 때 주로 패키지들의 버전 관리 등을 위해 가상 환경을 주로 사용하는 편인데(의존성 충돌 등을 피하기 위해는 거의 필수적이다), 
conda의 경우 온갖 패키지들이 다 들어있어서 무거운 편이라 회피하는 편이다. miniconda라고 하더라도 무겁게 느껴지기도 해서, 가상환경을 쉽게 관리할 수 있는 다른 방식을 채택했다.

바로 <span style="color: red; font-weight: bold;">venv</span>를 이용하는 방법이고 가볍다는 장점이 있으며, python 설치 시 내장 모듈이기 떄문에 손쉽다는 장점이 있다. 

## 가상환경 설정 및 활성화

### 가상환경 생성

```shell
cd <프로젝트 디렉토리>
python -m venv <가상환경 이름>
echo <가상환경 이름> >> .gitignore
```

해당하는 프로젝트 디렉토리로 이동해서, python의 내장모듈 venv를 이용해 가상환경을 생성해주면 된다.
가상환경의 경우에는 굳이 git에 올라가지 않아도 되기 때문에 .gitignore에 추가해준다.


### 가상환경 활성화

```shell
source <가상환경이름>/bin/activate
```

이런식으로 생성한 가상환경을 활성화시킬 수 있다. 


## 가상환경 코드에디터에 연결

나는 개발을 할 때, **Visual studio code**도 많이 사용하고 가볍게 상호작용성 코딩을 할 땐 **Jupyter**도 많이 사용하는 편이다.
그렇기에 두 코드 에디터 모두에 이 가상환경을 연결하는 방법을 작성해보고자 한다.

### Visual studio code 

(Mac 기준) `command + shift + P`를 입력해서 `Python: Select Interpreter`를 선택한다.
![VSCode select interpreter](/232319173-9989b6a9-d52f-49f5-937c-2b70b425398a.png)

그 후 뜬 목록에서 아까 생성한 python을 선택해주면 된다
![python 선택](/232319290-93488289-f5b9-42be-8cf9-44d4f1bb2123.png)

그 후에 새로 터미널을 열게 되면 이렇게 올바르게 가상환경이 잘 연결되었다. 
![python 연결완료](/232319346-ce830de1-d80b-48b5-85ac-e54473931de0.png)

### Jupyter lab

jupyter lab을 사용하기 위해선 해당 가상환경에 **ipykernel**을 설치해야한다.
우선 `source <가상환경 이름>/bin/activate`를 통해 가상환경을 활성화 시켜준 후 
```shell
pip install ipykernel
```
을 통해 설치해준다. 그 후 jupyter lab에 보여질 kernel을 추가해주면 된다. 아래와 같은 명령어이다.
```shell
python -m ipykernel install --user --name <가상환경 이름> --display-name <Jupyter lab에서 보여질 이름>
```

그 후 Jupyter lab을 실행시켜주면(`jupyter lab`) 아래 그림과 같이 jupyter lab에도 잘 연결되었다.
![jupyter lab python 연결](/232319563-3a2dd589-72a1-4449-844a-a95dfc8a5d61.png)

<br />
<div align="center" style="font-weight: bold;">
이렇게 python 가상환경을 만들고 사용하는 코드 에디터에 연결하는 방법까지 마무리했다 🩵
</div>



