---
title: "[유데미(Udemy)] React Native - 완벽가이드 [2024] 강의 후기"
date: 2024-04-11 22:00:00 +0900
categories: [React Native]
tags: [tech, reactnative, javascript, udemy]
---

![udemy-image](../../assets/img/posts/tech/udemy-image.png){: height="300"} 

## **수강한 강의 링크**
<https://www.udemy.com/course/react-native-2022-ko/>  
<br>

## **개요**
리액트 네이티브는 페이스북이 개발한 오픈 소스 모바일 애플리케이션 프레임워크입니다. 이는 안드로이드, iOS, 웹, UWP용 애플리케이션을 개발하기 위해 사용되며, 개발자들이 네이티브 플랫폼 기능과 더불어 리액트를 사용할 수 있게 합니다.  
React Native는 React를 배웠던 분들이라면 몇시간만에 익숙해질 수 있을만큼 유사한 문법을 지니고 있습니다.  

**<span style="background-color: #fff5b1;">유데미(Udemy)의 '[한글자막] React Native - 완벽가이드[2024]' 강의</span>**에서는 PUSH 알림, 훅, Redux를 포함한 React Native 및 React 지식을 통해 네이티브 iOS 및 Android 앱을 구축하는 방법을 배울 수 있습니다!  
저는 개인적으로 React Native로 앱을 개발 및 출시하고 나서 이 강의를 봤는데, 확실히 혼자 공부했을 때 놓쳤던 부분들이나 몰랐던 부분들을 채울 수 있었습니다.  
<br>

## **전박적인 강의 구성**

전반적으로 강의 구성을 설명하자면, 이 강의에서는 **React Native 컴포넌트로 사용자 인터페이스를 구축하는 법**과 **사용자 인터페이스의 스타일을 변경하고 효과적인 레이아웃을 구축하는 법**을 실제 앱을 구축해보면서 연습해 볼 예정입니다.  

또 내비게이션을 추가해서 사용자가 멋진 애니메이션과 함께 다양한 화면 간 전환할 수 있도록 만들고 Drawer 메뉴와 탭을 추가하는 법을 배울 것입니다.  

**<span style="background-color: #ffdce0;">이 강의를 최대한으로 습득할 수 있으려면 JavaScript와 React.js를 이미 알고 있어야 합니다.</span>**  
강의 막바지에 두 개의 복습 섹션이 있으니 React Native 섹션을 시작하기 전에 복습을 원한다면 우선 듣고 오셔도 된다고 합니다.  

React Native의 핵심을 배운 후에는 심화 기능으로 넘어갈 것입니다. 이때, 구체적으로 React 핵심 개념과 React Native가 어떻게 연관되어 있는지 그리고 Context API와 Redux 등을 React Native에서 사용하는 방법을 배울 것입니다.  

또 사용자 입력값을 처리하고 HTTP 요청을 보내는 등 여러 현식적인 앱을 구축해볼 것입니다. 더 나아가 심화 모듈에서는 사용자 인증이나 기기의 네이티브 기능을 활용하는 법을 배워볼 것입니다. 여기서 네이티브 기능에는 스토리지, 카메라, 사용자 위치, 지도 공유 및 PUSH 알림을 추가하는 방법 등이 있을 것입니다. 그리고 PUSH 알림을 추가하는 방법도 알아볼 것입니다.  

마지막으로 React Native 앱을 앱스토어에 출시하는 법을 배울 것입니다.  
<br>

## **React와 React Native의 차이**
React와 달리 React Native는 DOM을 가지고 있지 않으니 **HTML 요소를 지원하지 않습니다.**  
React Native는 React보다 엄격해서 View에서는 텍스트를 넣을 수 없습니다. 왜냐하면 **용도가 다르기 때문입니다.**  

React Native 세계에서는 div와 똑같은 **View는 일반적으로 콘텐츠를 담는 상자나 컨테이너를 구축하는 데 사용**됩니다. View에는 Text 컴포넌트로 묶인 텍스트를 넣을 수 있습니다.
```javascript
import { Text, View } from 'react-native';

const MyApp = () => {
  return (
    <View>
      <Text>Hello, world!</Text>
    </View>
  );
};
```

<br>

그리고 React Native에서는 **StyleSheet를 사용**합니다. 그 이유는 JSX 코드와 스타일 코드를 명확히 구분해주고 스타일을 재사용할 수 있기도 하지만 다음과 같은 장점들도 있기 떄문에 사용합니다.

- 스타일 프로퍼티를 입력할 때, 편리한 자동 완성 기능으로 개발 작업이 조금 더 쉬워진다.
- 추가로 React Native는 스타일 시트 생성과 관리를 내부적으로 최적화하고 StyleSHeet 객체를 인식하는 기능이 있습니다.
(StyleSheet 객체는 자동 완성 기능 말고도 코드 검증 기능도 있다. 잘못된 스타일 객체나 값에 오류나 경고를 표시해준다.)
- StyleSheet을 통해 유효성 검증을 할 수 있고, 성능 향상에도 도움을 줄 수 있습니다.

<br>

## **React Native 원리**
사용한 JSX 요소는 각 플랫폼의 네이티브 요소로 컴파일된다.

Web Browser | Native Component | Native Component | React Native JSX
(react-dom) | (Android) | (iOS) | 
:---:|:---:|:---:|:---:
`<div>` | android.View | UIView | `<View>`
`<input>` | EditText | UITextField | `<TextInput>`
... | ... | ... | ...

React Native는 재사용 가능한 컴포넌트를 매핑하고 컴파일한다.  
<br>

## **로직은 어떨까?**
UI 요소와 다르게 논리는 컴파일되지 않는다. React Native의 컴포넌트인 UI 요소는 컴파일된다.  

JavaScript에서 작성한 논리는 **컴파일되지 않고**, 구축한 네이티브 앱 안에서 React Native가 호스트한 대로 JavaScript 스레드에서 실행된다.

즉 React Native는 간단한 JavaScript 프로세스를 구축하고 네이티브 앱의 일부로 만들어 자동으로 이 프로세스를 관리해 네이티브 플랫폼과 상호작용할 수 있도록 한다.  

따라서 JavaScript 코드는 구축하고 있는 네이티브 앱 안에서 JavaScript 그대로 실행하면서 네이티브 앱의 React Native를 통해 언어의 장벽을 넘어 Android나 iOS 플랫폼과 상호작용한다.  

React Native를 다루기 위해서 이 정도만 알고 있으면 된다.  
<br>

## **React Native 앱 구축하는 2가지 방법**

React Native 앱을 구축하기 위해서는 2가지 방법이 있다.
CLI는 Command Line Interface로, 명령 행 인터페이스의 약자이다. 두 가지 툴 모두 React Native 프로젝트를 생성하고 테스팅 기기 및 시뮬레이터에 React Native 앱을 실행할 뿐만 아니라 React Native 앱을 구축하는 데 사용되어 앱스토어에 앱을 배포할 수 있도록 한다.  
실질적으로 앱을 구축하고 배포 가능한 패키지로 만들어 앱 스토어에 업로드하기 위해 꼭 필요한 툴이다.  

- **Expo CLI("Expo") Quickstart**
  - 서드 파티 서비스(무료)
  - 제공하는 몇 가지 무료 툴을 이용하면 "정리된 앱 개발" 워크플로우로 작업할 수 있다.
  - Expo 없이 React Native CLI만 사용하는 것보다 훨씬 편리하고 과정이 수월해진다.
  - 필요하다면 언제든지 Expo 방식을 중지해도 된다는 것이다. 

> 정리된 앱 개발이란?
> 프로젝트 생성이 수월하고 코드 작성이 역시 비교적 쉬우며 네이티브 기기의 카메라 등 기능을 활용하는 것이 전반적으로 쉬워진다.
{: .prompt-info }

- **React Native CLI Quickstart**
  - React Native 팀과 관련 커뮤니티가 제공한 툴이다. 
  - 기초적인 React Native 개발 설정을 제공한다. 이 말은 여기에 추가적인 구성 및 설정을 직접해야 한다는 뜻이다. 
  - 편리한 기능도 적고, 카메라 등 특정 네이티브 기기 기능을 활용할 때, Expo로 작업할 때보다 작업이 더 번거롭다. 
  - Java, Objective-C, Swift, Kotlin과 같은 네이티브 소스 코드와 통합하기가 비교적 쉽다.
  
<br>

## **강의 후기**
강의는 전반적으로 강사님이 친절하게 설명해 주셨고, 중요한 개념들을 ppt로 별도로 설명해 주셔서 매우 도움이 되었습니다. 특히, flex Box에 대한 설명은 제가 정확히 이해하지 못했던 부분이었는데, 이를 명확하게 설명해 주셔서 큰 도움이 되었습니다.  

강사님은 영어로 강의하셨지만, 번역이 잘 되어 있어서 이해하는 데 어려움이 없었습니다. 또한, 강의 중간중간 제공된 퀴즈를 통해 핵심 내용을 다시 상기할 수 있었던 점도 매우 유익했습니다.  
<br>

> 해당 콘텐츠는 유데미로부터 강의 쿠폰을 제공받아 작성되었습니다.

