---
layout: post
title:  "window terminal1.0 color change"
date:   2020-05-25 11:09:00 +0900
categories: 
---
![800x800](../assets/img/blog/windowterminal1.png "image1")

이번에 윈도우 터미널이 1.0으로 업데이트 되면서 좋아졌다 하길레 사용해보려 합니다.
사실 윈도우 터미널의 존재를 모르고 살고 필요성을 많이 못느꼈습니다..
기본 IDE에 power shell 이 붙어서 나오기 때문에 거기서 프로젝트를 빌드하고 사용했기 때문입니다..

[link](https://devblogs.microsoft.com/commandline/windows-terminal-1-0/)


윈도우 1.0 이 나왔다고 알리는 글입니다. 짧은 영어로 조금 읽어보면 윈도우 터미널은 2019년 나왔다고 하네요 1.0을 알리게 되어서 매우 자랑스럽다고 합니다. 윈도우 터미널은 마이크로소프트 스토어에서 다운 받을 수 있고 깃허브에서 오픈소스로 관리 된다 합니다. 저도 컨트리뷰션 해보고 싶네요! 

[link](https://learn.microsoft.com/ko-kr/windows/terminal/)


window terminal (윈도우 터미널) doc 링크 입니다. 
작업 흐름을 개선 해줄 여러 특징 들이 있다 하네요 ? command line app 을 실행할 수 있다하고.. .. GPU 가속 랜더링..
그렇다고 합니다.. 천천히 알아 봐야 겠어요 !
자 일단 색깔부터 바꾸고 시작해봐요.

![800x800](../assets/img/blog/windowterminal2.png "image1")

 기본 화면입니다.. 뭐 깔끔하네요 !

![800x800](../assets/img/blog/windowterminal3.png "image1")

위쪽에 화살표를 누르게 되면 설정 버튼이 있습니다. 저는 visual studio 가 깔려있어서 기본으로 vs 가 열리는데 안깔려 있으신분들은 어떨지 모르겠습니다. 

C:\Users\User\AppData\Local\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState

경로로는 이렇게 되어있네요 !  User부분을 맞게 수정해보세요 !

![800x800](../assets/img/blog/windowterminal4.png "image1")

list 부분에 power shell 의 color를 바꿔 보아요.

 

그러려면 schemes 부분에 스키마가 등록 되어있어야 합니다. 

 

찾아보니 여러 스키마를 제공하고 있는 open source 가 있습니다. 

 

https://atomcorp.github.io/themes/

![800x800](../assets/img/blog/windowterminal5.png "image1")

![800x800](../assets/img/blog/windowterminal6.png "image1")


그 후 복사한 theme을 schemes 에 붙여 넣어 주시고 power shell 부분에 

 
```
"colorScheme": "COLOR SCHEME NAME"
```
 
 입력 하시면 됩니다!

 

ubuntu theme 올려드리겠습니다.

```
    {
      "name": "Ubuntu",
      "black": "#2e3436",
      "red": "#cc0000",
      "green": "#4e9a06",
      "yellow": "#c4a000",
      "blue": "#3465a4",
      "purple": "#75507b",
      "cyan": "#06989a",
      "white": "#d3d7cf",
      "brightBlack": "#555753",
      "brightRed": "#ef2929",
      "brightGreen": "#8ae234",
      "brightYellow": "#fce94f",
      "brightBlue": "#729fcf",
      "brightPurple": "#ad7fa8",
      "brightCyan": "#34e2e2",
      "brightWhite": "#eeeeec",
      "background": "#300a24",
      "foreground": "#eeeeec"
    }

```

![800x800](../assets/img/blog/windowterminal7.png "image1")

네 잘 바뀌었습니다