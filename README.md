# MEMO IN THE AIR

<br>
<div align="center">
  <img src="./assets/images/new-logo.png" width="80%" alt="앱 로고">
</div>
<br>
<div align="center">
  <b>증강 현실(AR) 속 원하는 위치에 메모를 기록</b>하는 React Native 모바일 애플리케이션
  <br>
  -
  <br>
  기록을 위한 방법에는 글쓰기, 사진 찍기, 그림 그리기 등 다양한 방식들이 있으며,<br>이를 저장할 수 있는 모바일 애플리케이션 또한 많습니다.
  <br>
  <br>
  저는 기존의 방식과는 다른 색다른 방법을 고민하던 중 <br>
  “내 주변에 가상의 메모를 띄워서 보여주는 건 어떨까?”라는 생각을 하게 되었고,<br> 이 생각을 바탕으로 AR 메모 애플리케이션을 기획하게 되었습니다.
</div>

<br>
<br>
<br>

# 목차

<!-- toc -->

- [AR과 VR의 차이점](#ar%EA%B3%BC-vr%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- [기술 스택](#%EA%B8%B0%EC%88%A0-%EC%8A%A4%ED%83%9D)
  - [App](#app)
  - [Web](#web)
- [UI 미리보기](#ui-%EB%AF%B8%EB%A6%AC%EB%B3%B4%EA%B8%B0)
- [구현 기능](#%EA%B5%AC%ED%98%84-%EA%B8%B0%EB%8A%A5)
  - [회원가입 하지 않고 메모 저장하기](#%ED%9A%8C%EC%9B%90%EA%B0%80%EC%9E%85-%ED%95%98%EC%A7%80-%EC%95%8A%EA%B3%A0-%EB%A9%94%EB%AA%A8-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0)
  - [WebView에서 AR화면을 띄우는 이유](#webview%EC%97%90%EC%84%9C-ar%ED%99%94%EB%A9%B4%EC%9D%84-%EB%9D%84%EC%9A%B0%EB%8A%94-%EC%9D%B4%EC%9C%A0)

<!-- tocstop -->

<br>

# AR과 VR의 차이점

- AR(Augmented Reality) : 증강 현실
  - 현실 배경 또는 이미지에 컴퓨터가 만든 가상의 정보를 덧띄우는 기술
- VR(Virtual Reality) : 가상 현실
  - 컴퓨터를 통해 만들어진 가상 세계를 사용자에게 제공하여 가상 세계를 현실처럼 생생히 체험할 수 있는 기술

**MEMO IN THE AIR**은 사용자의 휴대폰 카메라를 통해 특정 위치에서 가상의 메모를 띄우고 확인하는 AR 애플리케이션입니다.

<br>

# 기술 스택

### App

<img src="https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React"/> <img src="https://img.shields.io/badge/React_Native-61DAFB?style=flat-square&logo=react&logoColor=black" alt="React Native"/> <img src="https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white" alt="Expo" /> <img src="https://img.shields.io/badge/Firebase-FFCA28?style=flat-square&logo=firebase&logoColor=black" alt="Firebase" /> <img src="https://img.shields.io/badge/Typescript-3178C6?style=flat-square&logo=Typescript&logoColor=white" alt="TypeScript"/> <img src="https://img.shields.io/badge/Zustand-443E38?style=flat-square" alt=”zustand”/>

### Web

<img src="https://img.shields.io/badge/AR.js-7FB8E3?style=flat-square" alt=”arjs”/>

<br>
<br>

# UI 미리보기

<table>
  <tr>
    <td width="33%">메인 화면</td>
    <td width="33%">AR 화면</td>
    <td width="33%">AR 화면 - 그리드</td>
  </tr>
  <tr>
    <td>
      <img width="100%" src="./assets/images/docs/main.png" alt="main">
    </td>
    <td>
      <img width="100%" src="./assets/images/docs/arView.png" alt="main">
    </td>
    <td>
      <img width="100%" src="./assets/images/docs/arView-grid.png" alt="main">
    </td>
  </tr>
  <tr>
    <td width="33%">메모 등록 화면</td>
    <td width="33%">사용자 위치 파악 화면</td>
    <td width="33%">메모 목록 화면</td>
  </tr>
  <tr>
    <td>
      <img width="100%" src="./assets/images/docs/createMemo.png" alt="main">
    </td>
    <td>
      <img width="100%" src="./assets/images/docs/location.png" alt="main">
    </td>
    <td>
      <img width="100%" src="./assets/images/docs/map.png" alt="main">
    </td>
  </tr>
</table>

<br>

# 구현 기능

## 회원가입 하지 않고 메모 저장하기

UUID와 expo-secure-store를 활용하여 회원가입 없이도 서비스를 이용할 수 있도록 했습니다.

기획 단계에서 앱스토어에 등록된 무료 메모 앱들을 파악했을 때, 회원가입이나 로그인없이도 서비스를 제공하는 앱이 많다는 점을 확인했습니다. 해당 사항을 참고하여 누구나 자유롭게 AR 기능을 체험하고 메모를 자유롭게 등록할 수 있도록, 회원가입 없이도 사용할 수 있는 앱을 기획하게 되었습니다.

이를 위해선 다음 두 가지 조건을 충족해야 했습니다.

1. 사용자를 식별할 수 있는 고유 정보를 파악할 수 있어야 한다.
2. 앱 종료 후에도 고유 정보를 기억하여, 재실행 시에도 동일 사용자로 파악되어야 한다.

<br>

**사용자 고유 정보 파악하기**

React Native 앱에서는 디바이스의 정보를 파악할 수 있는 `expo-device` 라이브러리가 있지만, 디바이스의 고유 ID를 제공하지 않기 때문에 적합하지 않았습니다. 이에 따라, 고유성이 보장되는 UUID 버전 4를 사용하여 앱 실행 시 사용자별 고유 ID를 생성하는 방법을 채택하였습니다.

<details>
  <summary>UUID 생성 코드</summary>
  <div markdown="1">

    import { v4 } from "uuid";

    export function createUUID(): string {
      return v4();
    }

  </div>
</details>

<br>

**앱이 사용자 ID를 계속 기억하기**

사용자의 고유 ID는 앱 종료나 재실행시에도 유지되어야 했습니다. 기존에 저장된 ID가 없다면 신규 사용자로 인식하고 ID를 생성하며, 이미 저장된 ID가 있다면 기존 사용자의 ID를 불러와야 합니다. 이를 위해 `expo-secure-store` 라이브러리를 활용했습니다.

`expo-secure-store` 라이브러리는 데이터를 암호화하여 키-값 조합으로 디바이스에 영구적으로 저장하는 기능을 제공하므로, 앱이 업데이트됙나 종료되어도 데이터를 안전하게 유지할 수 있습니다. 이러한 특성 덕분에 해당 라이브러리를 채택하게 되었습니다.

<details>
  <summary>expo-secure-store를 통해 사용자의 ID를 앱에 저장하는 코드</summary>
  <div markdown="1">
    
    import * as SecureStore from "expo-secure-store";
  
    export async function checkUserId(): Promise<string> {
      let userId: string | null = await SecureStore.getItemAsync("userId");
    
      if (userId === null) {
        userId = createUUID();
        await SecureStore.setItemAsync("userId", JSON.stringify(userId));
      }
    
      return userId;
    }
  </div>
</details>

<br>

**UUID**와 **expo-secure-store** 라이브러리를 함께 사용하여, 회원가입 없이도 사용자를 구분하고 사용자의 정보를 제공할 수 있는 구조를 구현하게 되었습니다.

## WebView에서 AR화면을 띄우는 이유

AR.js는 웹에서 AR를 구현할 수 있는 JavaScript 웹 라이브러리로, React Native에서 WebView를 사용하여 AR을 구현했습니다.

프로젝트 초기 단계인 PoC(Proof of Concept)에서 아래와 같은 이유로 'react-viro' 라이브러리를 선택하여 구현 가능성을 검토했습니다.

1. React Native 라이브러리로, 설치 이외의 추가적인 작업이 필요하지 않다.
2. AR 환경에서 텍스트나 도형 등의 물체를 자유롭게 수정 및 변형이 가능하며, 원하는 좌표에 물체를 위치시킬 수 있는 기능을 지원한다.

`react-viro`를 사용하여 구현 가능성을 확인했기에 구현 단계에서도 해당 라이브러리를 사용했습니다. `react-viro`를 사용하여 AR 화면을 띄우고 메모 위치를 보여주는 그리드를 구현하는 데 성공했으나, 다음 단계인 메모 등록 화면 기능을 추가하며 문제가 발생했습니다. AR 화면에서 메모 등록 화면으로 이동 시 앱이 강제 종료되는 현상이 확인되었습니다.

문제를 해결하기 위해 다음과 같은 사항들을 확인했습니다.

1. Router의 문제 여부

- AR 화면 외 다른 화면들 간의 이동은 정상적으로 동작했습니다.

2. 라이브러리 GitHub 이슈 확인

- 라이브러리의 GitHub 페이지에서 동일한 이슈를 발견했으나, 해결책에 대해선 답변이 없었습니다.

3. 라이브러리 버전 다운그레이드

- 라이브러리의 버전을 낮춰 테스트를 진행했으나 동일한 문제가 발생했습니다.

`react-viro` 라이브러리 자체 문제로 판단되었고 프로젝트 마무리까지 일주일밖에 남지 않은 상황이었기 때문에 라이브러리의 문제를 해결하는 데에 시간을 쓰는 것보단 새로운 방안을 찾아야 했습니다. React Native의 다른 AR 라이브러리는 이미 PoC 단계에서 확인했었기에 웹 AR 라이브러리인 `AR.js`를 사용하는 것으로 선택했습니다.

AR 환경을 구현하기 위해선 카메라를 사용해야 하는데 WebView에서 AR 웹 애플리케이션의 HTTPS 주소를 요구한다는 것을 확인했습니다. 따라서, 프로젝트 생성 후 `AR.js`의 테스트 코드로 먼저 배포하여 동작 여부를 확인했습니다. 테스트한 결과,
WebView 내에서 AR 화면이 정상적으로 실행되며, 페이지 간의 이동 또한 정상적으로 이루어졌습니다. 이에 따라 `AR.js` 라이브러리를 사용하여 프로젝트를 진행했습니다.

<br>
