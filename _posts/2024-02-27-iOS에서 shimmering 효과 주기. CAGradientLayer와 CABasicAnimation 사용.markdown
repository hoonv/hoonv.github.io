---
layout: post
title:  "iOS에서 shimmering 효과 주기. CAGradientLayer와 CABasicAnimation 사용"
date:   2024-02-27 00:00:00 +0900
categories: 
---
#### Shimmering 효과

![800x800](../assets/img/blog/shimmering_light.gif "image1")


Shimmer 효과는 사용자 인터페이스 디자인에서 로딩 중이거나 데이터를 기다리는 동안 사용자의 관심을 유지하기 위해 적용하는 시각적 피드백 방법입니다. 이 효과는 일반적으로 반짝이거나 빛나는 애니메이션으로, 화면의 특정 부분이나 텍스트, 이미지 등을 가로지르며 사용자에게 시각적으로 작업이 진행 중임을 알리는 효과가 있습니다.(로딩되고 있다 라는 피드백을 주는것이죠) 뿐만 아니라 사용자에게 특정한 영역을 보게 하게끔 사용자의 시선을 끄는 용도로 사용할 수 도 있습니다.
shimmer 효과 예시

#### CAGradientLayer 구현
CAGradientLayer와 CABasicAnimation을 활용하여 shimmering 효과를 구현하겠습니다. shimmering 효과의 핵심은 GradientLayer를 animation 시키는 것이여서요 먼저 GradientLayer를 만드는 코드를 살펴보겠습니다. GradientLayer에 대해서는 관련링크를 참고 부탁드립니다. apple문서-CAGradientLayer

```swift
let gradientLayer = CAGradientLayer()
let gradationColor = [UIColor.clear, .white.withAlphaComponent(0.15), .clear]
gradientLayer.frame = self.bounds
gradientLayer.startPoint = CGPoint(x: 0.0, y: 0.5)
gradientLayer.endPoint = CGPoint(x: 1.0, y: 0.5)
gradientLayer.colors = gradationColor.map { $0.cgColor }
gradientLayer.locations = [-0.5, -0.25, 0]
self.layer.addSublayer(gradientLayer)
````

gradientLayer의 bounds 내의 locations 값은 0~1 사이의 값으로 정의해주면 되는데요. 저는 여기서 초기엔 gradientLayer가 보이지 않았으면 해서 -0.5~0으로 설정해주었습니다. 또한 범위를 0.5만큼 잡은것은 shimmering할때 gradeintLayer를 기준 View의 반 만큼만 Gradient를 주고 싶어서 범위를 0.5만큼만 설정해주었습니다.

#### CABasicAnimation 구현

```swift 
let animation = CABasicAnimation(keyPath: "locations")
animation.fromValue = [-0.5, -0.25, 0]
animation.toValue = [1, 1.25, 1.5]
animation.timingFunction = CAMediaTimingFunction(name: .easeOut)
animation.repeatCount = 2
animation.duration = 3.5
gradientLayer.add(animation, forKey: "shimmering")
```
layer에 animation을 add 하면 바로 animation이 동작합니다. 여기서 조금 특이한것은 fromValue, toValue의 값이 0미만 1초과 된 값으로 사용했는데 그 이유는 gradient의 너비를 위에서 View의 너비의 50%로 설정을 했는데요, 이 gradient가 animation이 시작하면서 서서히 보이고 또 완전히 사라지게 하기 위해 위와 같이 value를 설정 해주었습니다. 이거는 각각 상황에 맞게 커스텀해서 사용하면 될것 같습니다.

감사합니다.