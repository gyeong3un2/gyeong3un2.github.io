---
title: "[Udemy] React Native Section 1.1 ~ 1.5"
date: 2023-12-15 03:00:00 +0900
categories: [React Native]
tags: [tech, reactnative, javascript, udemy]
---

ReactJS와 React Native를 함께 사용하면 React Native를 기반으로 한 iOS와 Android용 모바일 앱을 구축할 수 있다.  

ReactJS는 인터페이스 구축을 위한 JavaScript 라이브러리이다. 보통 웹 개발에 사용된다.  
React Native에 내장된 컴포넌트들은 iOS 및 Android 플랫폼을 위해 네이티브 UI 요소로 컴파일된다.  
기기의 카메라를 사용하는 등 특정 네이티브 플랫폼 API를 노출해서 JavaScript 코드에서 해당 기능을 사용할 수 있도록 한다. 이때 네이티브 기기 API를 켜야 하기는 하다. 플랫폼 대상은 iOS와 Android이다.  

ReactJS에서 코드를 작성한 후, React JavaScript 코드에서 React Native 컴포넌트와 API를 추가로 사용해 iOS 및 Android의 네이티브 모바일 앱을 제작하기 때문이다.  
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

