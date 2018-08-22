---
layout: post
title: How to install clang++ and llvm.
subtitle: step by step install guide
category: [etc, ]
tags: [ubuntu, llvm, clang++, ]
---

vscode 환경설정위해 llvm, clang을 install하고자 한다.
공식홈페이지는 [*이곳*](http://apt.llvm.org/) 이다.

----

1) 먼저 홈페이지에 접속해서 signature를 받아온다.
`$ wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -`

2) repository 추가
`$ sudo vim /etc/apt/sources.list` 파일 열어서 제일 아랫줄에 추가.
`deb http:// apt.llvm.org/bionic/ llvm-toolchain-bionic-6.0 main`
`#deb-src http:// apt.llvm.org/bionic/ llvm-toolchain-bionic-6.0 main`

3) package index update.
`$ sudo apt-get update`

4) clang, llvm install
`$ apt-get install clang-6.0 clang-tools-6.0 libclang-common-6.0-dev libclang-6.0-dev libclang1-6.0 libllvm-6.0-ocaml-dev libllvm6.0 lldb-6.0 llvm-6.0 llvm-6.0-dev llvm-6.0-runtime clang-format-6.0 python-clang-6.0 lldb-6.0-dev lld-6.0 libfuzzer-6.0-dev`

## 2. install oh-my-zsh.

curl을 사용하여 명령어 한 줄로 설치할 수 있다.  
`$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`

## 3. Customizing.

지금부턴 shell을 좀 더 예쁘게 꾸미기 위한 팁...  
이걸 해주면 아주 좋다.

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