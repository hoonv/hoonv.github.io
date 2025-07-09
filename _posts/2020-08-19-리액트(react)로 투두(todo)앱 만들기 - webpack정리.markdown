---
layout: post
title:  "리액트(react)로 투두(todo)앱 만들기 - webpack정리"
date:   2020-08-19 18:22:00 +0900
categories: 
---

![800x800](../assets/img/blog/react01.png "image1")

프로젝트를 진행하다 보니 자잘자잘하게 웹팩 설정 할 것이 많아서 한번에 정리하고자 합니다. 포스팅을 진행하면서 저도 조금더 웹팩에 대해 공부를 하게 되었데요. 사실 웹팩은 저희가 진행하는 토이프로젝트에는 맞지 않는다는 생각을 했습니다. 웹팩의 역할은 많은 js파일 css파일 png파일들을 묶어주는 것인데요. 저희가 진행하는 프로젝트는 규모가 너무 작아서 사실 기술의 편안함 보다는 진입장벽으로 다가오는게 현실이죠.. 

 

하지만 웹팩은 꼭 필요한 기술이므로 지금부터 천천히 익혀나가는게 중요하다고 생각합니다.! 웹팩은 큰그림으로 보자면 정말 어려울게 없는 기술입니다. 엔트리지점을 정해서 그것과 연관된 모든 파일을 찾아서 묶어주는것이죠. 묶을때 파일별로 묶어줍니다. 그것을 webpack.config.js 파일에서 결정해주는것이죠 예를들면 .scss파일은 어떠한 loader로 묶어줘라 png jpg파일들은 어떠한 loader로 묶어줘라 그리고 파일들을 묶을때 여러 도움을 주는 plugin을 사용해서 묶어주는것입니다. 그 후 output폴더에 어떠한 이름으로 정할지 정해주는것입니다. 그리고 어떠한 확장자는 확장자 명시없이 import할지 지정할 수 도 있습니다. 그것을 코드를 보며 다시 확인을 해보겠습니다. 

 
```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin')

module.exports = {
  entry: './index.tsx',
  output: {
    path: path.join(__dirname, '/dist'),
    filename: 'index_bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/,
        use: [
          'babel-loader',
          {
            loader: 'ts-loader',
            options: {
              transpileOnly: true
            }
          }
        ],
        exclude: /node_modules/
      },
      {
        test: /\.scss$/,
        use: [
          'style-loader', // creates style nodes from JS strings
          'css-loader', // translates CSS into CommonJS
          'sass-loader' // compiles Sass to CSS, using Node Sass by default
        ],
        exclude: /node_modules/
      },
      {
        // write image files under 10k to inline or copy image files over 10k
        test: /\.(jpg|jpeg|gif|png|svg|ico)?$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 10000,
              fallback: 'file-loader',
              name: 'images/[name].[ext]'
            }
          }
        ]
      },
      {
        // write files under 10k to inline or copy files over 10k
        test: /\.(woff|woff2|eot|ttf|otf)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 10000,
              fallback: 'file-loader',
              name: 'fonts/[name].[ext]'
            }
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html'
    }),
    new ForkTsCheckerWebpackPlugin({ silent: true })
  ],
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx']
  }
}
 ```

일단 제가 셋팅한 webpack.config.js 파일입니다.  

 
```
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')
const ForkTsCheckerWebpackPlugin = require('fork-ts-checker-webpack-plugin')
```
웹팩을 진행하는데 있어서 도움을 주는 plugin들입니다

HtmlWebPackPlugin 은 웹팩이 html 파일을 읽어서 웹팩으로 만든 번들링된 파일을 사용하는 html파일로 만들어 줍니다. 

forktscheckerwebpackplugin은 Webpack plugin that runs TypeScript type checker on a separate process.로 타입체킹을 더 빨리 해주는 플러그인입니다. 

 
```
module.exports = {
  entry: './index.tsx',
  output: {
    path: path.join(__dirname, '/dist'),
    filename: 'index_bundle.js'
  },
}
 ```

웹팩하는데 있어서 입구와 출구를 정해주는 코드입니다. entry는 프로젝이 root 파일을 상대경로로 적어주시면되고 output에는 path와 filename을 정해주시면 됩니다. 

 
```
module.exports = {
...
  module: {
    rules: [
      {
        test: /\.(ts|tsx)$/,
        use: [
          'babel-loader',
          {
            loader: 'ts-loader',
            options: {
              transpileOnly: true
            }
          }
        ],
        exclude: /node_modules/
      },
      {
        test: /\.scss$/,
        use: [
          'style-loader', // creates style nodes from JS strings
          'css-loader', // translates CSS into CommonJS
          'sass-loader' // compiles Sass to CSS, using Node Sass by default
        ],
        exclude: /node_modules/
      },
      {
        // write image files under 10k to inline or copy image files over 10k
        test: /\.(jpg|jpeg|gif|png|svg|ico)?$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 10000,
              fallback: 'file-loader',
              name: 'images/[name].[ext]'
            }
          }
        ]
      },
      {
        // write files under 10k to inline or copy files over 10k
        test: /\.(woff|woff2|eot|ttf|otf)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 10000,
              fallback: 'file-loader',
              name: 'fonts/[name].[ext]'
            }
          }
        ]
      }
    ]
  },
...
}
 
```
웹팩의 핵심인 rule 부분입니다. 웹페이지를 만드는데 있어서 필요한 여러파일을 확장자 별로 어떠한 loader를 이용하여 웹팩을 진행할지 명시하는 부분입니다 

 
```
module.exports = {
 ...
  plugins: [
    new HtmlWebpackPlugin({
      template: './index.html'
    }),
    new ForkTsCheckerWebpackPlugin({ silent: true })
  ],
  resolve: {
    extensions: ['.js', '.jsx', '.ts', '.tsx']
  }
}
 ```

마지막으로 plugin들을 사용하는곳과 웹팩이 어떤 확장자를 처리해줄지 도와주는 옵션입니다. 