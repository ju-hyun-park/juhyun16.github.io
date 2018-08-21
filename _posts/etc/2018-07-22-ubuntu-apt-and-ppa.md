---
layout: post
title: How to uninstall packages on ubuntu
subtitle: instructions of PPA and APT
category: [etc, ]
tags: [ubuntu, apt, ppa, ]
---

## 0. APT and PPA...

Debian 계열의 리눅스 시스템에서는 주로 APT(Advanced Package Tool)와 PPA(Personal Package Archive)를 사용해서 필요한 패키지들을 install 하게 되는데 몇 가지 중요한 명령어들만 정리해보고자 한다.

- `apt-get update` : **package index**를 업데이트 한다. 현재 시스템에 install되어 있는 모든 package에 대하여 이 package들이 새 버전으로 upgrade 되었는지 아닌지 체크한다. `/etc/apt/sources.list` 파일에 있는 서버에 접속하여 확인한다.

- `apt-get upgrade` : 실제로 package upgrade를 한다. `apt-get update` 에선 index만 업데이트 했고 실제 package upgrade는 이 명령을 통해 이루어진다!

- `apt-get dist-upgrade` : 의존성있는 패키지들도 모두 업그레이드 한다. 즉, A라는 package를 upgrade하려고 하는데 A package가 다른 B, C package에 의존성을 가지고 있는 경우 B, C 패키지까지 업그레이드 해주는 명령이 dist-upgrade 이다.

----------------------------------------------------

PPA를 사용하는 이유는 무엇일까? repository에 있는 software들은 stable version의 것들이다. 이 software들은 ubuntu team에서 철저히 관리한다. 다음과 같은 상황을 고려해보자. java의 새로운 버전이 출시되었다. 그런데 새 버전의 자바는 다음 버전의 우분투가 release되기 전까지는 repository에 등록되지 않는다.

몇몇 사용자들은 최신버전의 자바를 사용하길 원할 수 있다.(새 버전의 우분투가 나오기 전 이라도...)

이런 유저들의 needs에 맞춰서 자바 팀 에서는 자체적으로 패키지 저장소를 관리하는데 우리는 이를 통해서도 패키지를 설치할 수 있다.

- `add-apt-repository ppa:NAME` : ppa를 추가한다. `/etc/apt/sources.list.d` 파일에 ppa가 추가된다.
- `apt-get update` : 마찬가지로 package index를 update한다.
- `apt-get install name-of-package` : package install!!

참고 url : https://askubuntu.com/questions/825306/how-to-remove-pantheon-de-from-ubuntu-16-04


## 1. APT 명령으로 설치한 package 삭제하기.

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