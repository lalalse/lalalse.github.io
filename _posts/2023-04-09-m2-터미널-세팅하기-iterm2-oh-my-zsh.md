---
layout: post
title: M2 터미널 세팅하기 - iTerm2 + oh-my-zsh
subtitle: macOS의 기본 터미널보다 더 예쁘고 다양하게 기능할 수 있도록 iTerm 세팅
date: 2023-04-09 02:06 +0900
category: [macOS, setting]
tags: [terminal, mac, item2, oh-my-zsh]
---


## 기본 세팅

### 1. iTerm2 설치: [iTerm2](https://iterm2.com)
### 2. oh-my-zsh 설치: [oh-my-zsh](https://ohmyz.sh/#install)
- oh-my-zsh: zsh configuration 관리를 위한 프레임워크
- m2의 경우 기본 shell이 zsh로 설정되어있으므로 별도의 zsh 설치는 생략함

## iTerm2 커스텀하기 

### 1. D2 Coding 폰트 적용 
- D2 coding font 설치: [D2CodingFont](https://github.com/naver/d2codingfont)
    - ligature: 합자 기능으로 2개의 글자를 하나로 간결하게 합쳐서 표현하는 방법
        - 개발할 때는 오히려 불편할 수도 있을 것 같아서 ligature 말고 일반으로 사용하기로

- iTerm2에 폰트 적용
    - iTerm2 Preferences(command + , 또는 preferences)에서 폰트 변경
    ![iTerm2 Preference Font Setting](/230734842-696a0bab-6069-48bb-9d83-8d065090f66e.png)


### 2. Agnoster 테마 적용
- Agnoster 테마: git 사용 시에 유용, 현재 디렉토리의 상태 분기 등을 확인 가능하다는 장점
- 적용 방법
    1. `~/.zshrc`{: .filepath} 파일 편집 시작: `vi ~/.zshrc`
    2. `ZSH_THEME="agnoster"`로 변경
    3. `source ~/.zshrc`를 통해 적용하고 확인


### 3. 사용자 이름 설정
- 원하는 것: 기본적으로 못생긴 macbook 주저리주저리는 없애고 원하는 형태로 보여지게
- erin + (emoji) : emojis 목록을 주고 해당 목록에서 랜덤으로 픽해서 붙일 수 있도록 한다
- 적용 방법
    1. `vi ~/.zshrc`로 zshrc 편집 시작
    2. 
        ```
       prompt_context() {
            emojis=("🦖", "🫠 ", "💎", "❣️")
            RAND_EMOJI_N=$(( $RANDOM % ${#emojis[@]} + 1))
            prompt_segment black default "erin ${emojis[$RAND_EMOJI_N]}  "
       }
        ```
- 결과
  <br />
    ![사용자 이름 커스텀 결과](/230735714-99708ef6-015d-4eb2-aeed-26f515cf463d.png)


### 4. 기타 플러그인 적용
#### 4.1. syntax highlighting 
- syntax들에 다른 색깔로 highlighting을 해줌으로써 가독성을 높여준다
- 적용 방법
    1. `brew install zsh-syntax-highlighting`으로 설치
    2. `vi ~/.zshrc`를 통해 아래 코드 추가  
        `source /opt/homebrew/share/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh`
- 결과
    <br />
    ![syntax highlighting 적용 결과](/230735748-49f34fcd-8bb3-4549-bf5a-ab320c58182a.png)

#### 4.2. autosuggestions
- 최근 입력한 명령어 history를 통해 후보를 보여줌; 미리보기를 통해 선택 가능
- 적용 방법
    1. `brew install zsh-autosuggestions`로 설치
    2. `vi ~/.zshrc`를 통해 아래 코드 추가  
        `source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh`
- 결과 (*사실 그 사이에 color palette을 약간 바꿨다.*)
    <br />
    ![autosuggestions 적용 결과](/230735893-2813a251-0ff9-473a-997c-26fb98f04526.png)


<br />
<br />

<div align="center" style="font-weight: bold;">이렇게 내 맘에 쏙 드는 terminal을 완성할 수 있었다🩵</div>

