---
layout: post
title: How to setup Webstorm for competitive programming
subtitle: my custom setting of Webstorm for node js problem solving
category: [DEV, javascript, ]
tags: [node.js, webstorm, PS, ]
---

## 1. create project
웹 스톰을 열어서 `Create New Project` 를 클릭하여 제일 먼저 프로젝트를 만든다.  
이 때 **Empty Project**를 클릭한다.

## 2. disable auto save
preference > appearance & behavior > system settings 에 가서  
- [x] synchronize files on frame or editor tab activation  
- [x] use "safe write"  
위 두 항목을 체크한다.

<img src="{{site.url}}/img/2019-01/pic1.png" width="700" height="500" />

preference > editor > general > editor tabs 에 가서
- [x] mark modified (*)
항목을 체크한다.

<img src="{{site.url}}/img/2019-01/pic2.png" width="700" height="500" />

## 3. npm init
`npm init` 으로 npm package 설치를 위한 기본셋팅

## 4. eslint, prettier, babel 설정
prettier는 system에 global하게 설치한다.  
babel, eslint는 project directory에 설치한다. --save-dev  
세 도구 모두 webstorm preferences 에서 enable할 수 있다.

<img src="{{site.url}}/img/2019-01/babel.png" width="700" height="500" />

<img src="{{site.url}}/img/2019-01/prettier.png" width="700" height="500" />

<img src="{{site.url}}/img/2019-01/eslint.png" width="700" height="500" />

## 5. ~.rc.js 파일 설정
.eslintrc.js, .babelrc.js, .prettierrc.js 에 구체적인 셋팅을 한다.

`.eslintrc.js`
``` javascript
module.exports = {
  extends: ['airbnb-base', 'prettier'],
  rules: {
    quotes: 'off',
    'no-console': 'off',
    'func-names': ['error', 'never'],
    'no-unused-vars': 'warn',
    'no-use-before-define': 'off',
    'no-continue': 'off',
    'no-restricted-syntax': 'off',
    'no-bitwise': 'off',
    'no-param-reassign': 'off',
  },
};
```

`.babelrc.js`
``` javascript
const presets = ["@babel/env"];
module.exports = {presets};
```

`.prettierrc.js`
``` javascript
module.exports = {
  trailingComma: 'es5',
  singleQuote: true,
};
```

## 6. project directory 구조 잡기
src와 lib디렉토리를 만든다. 이젠 src/icpc 에 있는 파일들만 transpiling 되게 babel을 설정한다.  
babel 설정은 위의 5번을 참고하면 된다.

project working directory에 src와 lib디렉토리를 만든다.

## 7. Run / Debug main.js
readFileSync or fs.createReadFileStream 으로 바꾸고 main.js 파일 우클릭해서 실행 / 디버깅 할 수 있다.

``` javascript
const RL = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout,
});
```

위의 코드에서 `input: process.stdin` 을 `input: fs.createReadStream('./src/codeforces/1095/C/input.txt')` 이것으로 바꾼다.

main.js 파일을 우클릭해서 실행한다.

<img src="{{run}}/img/2019-01/run.png" height="800" />
