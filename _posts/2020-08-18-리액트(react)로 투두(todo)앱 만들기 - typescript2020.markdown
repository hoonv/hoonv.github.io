---
layout: post
title:  "리액트(react)로 투두(todo)앱 만들기 - typescript2020"
date:   2020-08-18 18:22:00 +0900
categories: 
---

![800x800](../assets/img/blog/react01.png "image1")

이번에는 타입스크립트를 적용시켜보겠습니다. 자바스크립트는 타입을 지정하지 않아도 되서 어떠한 변수가 string이었다가 number이였다가 자유자제로 바뀔 수 있습니다. 또한 컴파일 언어가 아니기 때문에 컴파일단계에서 에러를 확인 할 수도 없습니다. 이것을 해결하기 위해 자바스크립트 위에 타입을 지정해준것이 타입스크립트 입니다. 사전 컴파일을 한다고 생각하시면 될 것 같습니다. 

 

먼저 모듈부터 설치하겠습니다.

 
```
npm i -D typescript @babel/preset-typescript ts-loader fork-ts-checker-webpack-plugin
```

```
npm i @types/react @types/react-dom
```
기존에 적었던 코드를 하나씩 바꾸어 나가겠습니다. 

 

1. webpack.config.js
```
  entry: "./index.tsx",
...
  rules: [
    {
      test: /\.(ts|tsx)$/,
      use: [
        "babel-loader",
        {
          loader: "ts-loader",
          options: {
            transpileOnly: true
          }
        }
      ],
      exclude: /node_modules/
    }
  ]
    ...
plugins: [
  new HtmlWebpackPlugin({
    template: "./index.html"
  }),
  new ForkTsCheckerWebpackPlugin({ silent: true })
],
resolve: {
  extensions: [".js", ".jsx", ".ts", ".tsx"]
  }
```

2. tsconfig.json 파일을 생성합니다.

```
{
  "compilerOptions": {
    "target": "es6",
    "module": "esnext",
    "moduleResolution": "node",
    "noResolve": false,
    "noImplicitAny": false,
    "removeComments": false,
    "sourceMap": true,
    "allowJs": true,
    "jsx": "react",
    "allowSyntheticDefaultImports": true,
    "keyofStringsOnly": true
  },
  "typeRoots": ["node_modules/@types", "src/@type"],
  "exclude": [
    "node_modules",
    "build",
    "scripts",
    "acceptance-tests",
    "webpack",
    "jest",
    "src/setupTests.ts",
    "./node_modules/**/*"
  ],
  "include": ["./src/**/*", "@type"]
}
 ```

3.  .babelrc 파일을 수정합니다. 

```
{
  "presets": [
    [
      "@babel/preset-env",
      { "targets": { "browsers": ["last 2 versions", ">= 5% in KR"] } }
    ],
    "@babel/react",
    "@babel/typescript"
  ]
}
 ```

4. index.tsx 파일로 수정해줍니다. 

```
import React from "react";
import ReactDOM from "react-dom";

interface Props {}

const App = ({}: Props) => {
  return <h1>Hello World!</h1>;
};

ReactDOM.render(<App />, document.getElementById("app"));
 ```

이렇게 설정해주면 잘 실행된는것을 볼 수 있습니다. 