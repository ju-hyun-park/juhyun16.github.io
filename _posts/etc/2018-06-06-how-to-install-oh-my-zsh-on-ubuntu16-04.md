---
layout: post
title: How to install zsh, oh my zsh on ubuntu 16.04 LTS
subtitle: step by step install guide
category: [etc, ]
tags: [ubuntu, zsh, ]
---

## 1. install zsh.

`$ zsh --version` 으로 zshell 설치여부를 확인한다. 만약 install 되어 있지 않다면,  
`$ sudo apt-get install zsh` 으로 설치한다.  
개인 취향에 따라 zsh을 default shell로 설정할 수 있다.  
`$ chsh -s $(which zsh)`

{: .box-warning}
**Warning:** **재부팅**하여 zshell이 default로 지정되었는지 확인한다.

## 2. install oh-my-zsh.

curl을 사용하여 명령어 한 줄로 설치할 수 있다.  
`$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

## 3. Customizing.

지금부턴 shell을 좀 더 예쁘게 꾸미기 위한 팁...

`~/.zshrc` 파일을 열어서 테마를 바꾸자.  
`ZSH_THEME` 값이 default로 `robbyrussell`로 되어 있을 것이다.
아래와 같이 바꾼다.  
`ZSH_THEME="agnoster"`  

이어서 [*powerline Fonts*](https://github.com/powerline/fonts) 를 설치한다.  
 `sudo apt-get install fonts-powerline`

만약 터미널에서 보여지는 `username@computername $ ` 형태가 싫다면 `~/.zshrc` 파일을 열어서 다음의 코드를 추가해준다.

`DEFAULT_USER=$USER`

변경사항을 즉시 적용한다.  
`source ~/.zshrc`

The end.