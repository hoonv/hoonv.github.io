---
title: 커서에서 iOS앱 실행하기
author: hoonv
date: 2025-07-11 15:34:00 +0900
categories: [Swift, AI, iOS]
tags: []
---

대부분의 내용은 다음의 게시물을 참고하여 진행했습니다.
<https://velog.io/@cheshire0105/Xcode-with-Cursor> 


첫번째로 설치헤야 할것은 `xcode-build-server` 입니다.
```
brew install xcode-build-server
```
을 통해 설치할 수 있습니다. 간단히 해당 도구를 설치하는 이유를 간단히 설명 하자면, 먼저 LSP라는 것을 알아야 하는데요.
LSP란 language server protocol의 약자 입니다. XCode를 사용하다보면 코드의 자동완성이라던지, 이동, 정의 등 개발 하는데 있어서
편의사항을 제공하는데 이를 제공하는것이 language server 라고 생각하시면 되고 이를 protocol로 정의해둔것이 LSP 라고 생각하시면 될거 같아요.  
Swift는 lsp로 sourcekit-lsp가 있는데요. 기본적으로 xcode project를 지원하지 않아서 xcode-build-server가 나왔다고 보시면 됩니다.  
즉 해당 구현체를 통해 Xcode가 아닌 외부 에디터에서도 Swift 문법 자동완성이라던지 정의 점프 등이 가능합니다!    


```
brew install xcbeautify
brew install swiftformat
```
다음으로 XCBeautify는 xcodebuild 명령어의 출력 결과를 보기 쉽게 포매팅해주는 도구, SwiftFormat은 Swift 코드를 자동으로 포매팅해주는 라이브러리 및 CLI 도구를 설치하시면 됩니다. 개발하면서 출력이나 코드를 더 보기 좋게 해주는 것들이라고 해요~

그리고 cursor 에디터에서 extension을 설치하시면 됩니다.
- Swift Language Support
- Sweetpad

sweetPad 설치 및 빌드 셋팅은 원글을 보시는게 더 좋을거 같고. 저는 빌드 셋팅중에 아래와 같은 에러 로그가 발생했는데요,


```
time: 2025-07-11T05:54:38.314Z
level: ERROR
message: "Error executing "xcodebuild" command"
stackTrace: |
  Error: Error executing "xcodebuild" command
      at /Users/username/.cursor/extensions/sweetpad.sweetpad-0.1.66-universal/out/extension.js:235:5816
      at Generator.throw (<anonymous>)
      at s (/Users/username/.cursor/extensions/sweetpad.sweetpad-0.1.66-universal/out/extension.js:1:1421)
      at processTicksAndRejections (node:internal/process/task_queues:95:5)
context:
  logContext: {"command":"sweetpad.build.generateBuildServerConfig","errorContext":{"errorMessage":"Command failed with exit code 1: xcodebuild -list -json -workspace /Users/username/src/projectFolder/Project.xcworkspace","stderr":"xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance","command":"xcodebuild","args":["-list","-json","-workspace","/Users/username/src/projectFolder/Project.xcworkspace"],"cwd":"/Users/username/src/projectFolder"}}
  errorContext: {"context":{"errorMessage":"Command failed with exit code 1: xcodebuild -list -json -workspace /Users/username/src/projectFolder/Project.xcworkspace","stderr":"xcode-select: error: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance","command":"xcodebuild","args":["-list","-json","-workspace","/Users/username/src/projectFolder/Project.xcworkspace"],"cwd":"/Users/username/src/projectFolder"}}
```

현재 xcodebuild가 실행되면서 Xcode 전체가 아닌 “Command Line Tools”만 설치되어 있어서 실패하고 있었습니다.

```
xcode-select -p
// /Library/Developer/CommandLineTools 잘못된경로임!
```

아래와 같은 명령어 실행해서 Xcode로 연결해주면 됩니다.

```
sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
```

이후 문제 없이 커서에서 프로젝트가 빌드 됐습니다!