---
title: "프론트엔드 개발에서 MSW를 이용한 효과적인 API 모킹 방법"
date: 2024-05-26 20:15:00 +0900
categories: [Frontend]
tags: [Frontend, MSW, API Mocking]
---

## **API 모킹의 중요성**

대부분의 프론트엔드에서의 API 모킹은 개발 초기 단계에서 백엔드 API가 준비되지 않았을 때 MSW를 도입해서 사용합니다. 하지만, 이 API 모킹은 개발 중에도 매우 중요한 역할을 합니다.

에러를 발생시켜야 하는 환경, 로그인이 되었을 때의 화면 등을 테스트해보고 싶을 때 유용하게 사용할 수 있습니다.

왜냐하면 API 모킹을 통해 실제 백엔드 서비스 없이도 프론트엔드 서비스의 동작을 시뮬레이션할 수 있기 때문입니다.  
이는 개발 속도를 높이고, 백엔드와의 API 연동 부분에서 발생할 수 있는 문제를 사전에 발견하고 해결하는 데 도움을 줍니다.

<br><br>

## **MSW 소개**

MSW란 Mock Service Worker로, **브라우저와 Node.js 환경에서 네트워크 환경을 가로채고 모킹할 수 있는 라이브러리**입니다.  
MSW는 Service Worker API를 사용하여 실제 네트워크 요청을 가로채고, 개발자가 정의한 응답으로 대체하기 때문입니다.  
이를 통해 실제 백엔드 서버 없이도 API 요청과 응답을 시뮬레이션할 수 있습니다.

<br>

> **Service Worker란?**
>
> 최신 브라우저에서 지원되고 있는 기술로 웹 응용 프로그램, 브라우저, 그리고 (사용 가능한 경우) <u>**네트워크 사이의 프록시 서버 역할**</u>을 합니다.
>
> 이를 이용하면 네트워크 요청이나 응답을 가로채서 조작하는 것이 가능합니다. 이러한 특성을 이용해서 실제 API 요청이 발생했을 시 미리 준비해둔 Mock 데이터로 대신 응답을 보내는 방식을 사용하고 있습니다.

<br><br>

## **MSW 사용해보기**

### **MSW 설치**

```bash
$ npm install msw --save-dev
# or
$ yarn add msw --dev
```

<br>

### **Service Worker 등록**

브라우저에서 사용하기 위해서는 MSW를 Service Worker에 등록하는 과정이 필요한데, 아래의 명령어를 실행하면 Service Worker 등록을 위한 파일이 `public` 폴더 아래에 추가될 것입니다.

그렇게 되면 `/public/mockServiceWorker.js` 파일이 생성되며, `--save` 옵션을 사용하면 package.json에 등록되고 **msw를 업데이트할 때마다 자동으로 해당 항목을 업데이트**합니다.

<br>

> **mockServiceWorker.js 파일은 무슨 역할을 하나요?**
>
> 실제 서버로 보내지는 요청이 있다면, mockServiceWorker.js가 가로채서 mockServiceWorker에서 응답을 줍니다.

<br>

```bash
$ npx msw init public/ --save
```

<br>

### **MSW 세팅하기**

#### **🗒️ src/mocks/browser.ts**

MSW의 경우 service worker가 브라우저의 요청(CSR에서의 요청)을 뺏어서 browser.ts로 요청을 전달합니다.

```ts
import { setupWorker } from "msw/browser";
import { handlers } from "./handlers";

const worker = setupWorker(...handlers);

export default worker;
```

<br>

#### **🗒️ src/mocks/http.ts**

**Next.js는 서버와 클라이언트에서 동작하기 때문에 SSR 동작을 할 때에 서버에서도 MSW가 동작**해야 합니다.

서버와 클라이언트 두 곳에서 MSW가 동작해야 하는데 아직 서버에서 MSW를 동작시키는 방식이 나오지 않아(Next.js와 매끄럽게 호환되지 않음) Node 서버를 활용하여 임시로 MSW를 동작시킵니다.

즉, <u>**http.ts 같은 경우는 서버 컴포넌트에서 서버로 요청을 보낼 때, next 서버(SSR)에서의 요청을 모킹하기 위해 사용되었습니다.**</u>

```bash
# http-middleware: msw로 mock server를 만들기 위해 필요한 라이브러리
$ npm i -D @mswjs/http-middleware express cors @types/express @types/cors
```

```ts
import { createMiddleware } from "@mswjs/http-middleware";
import express from "express";
import cors from "cors";
import { handlers } from "./handlers";

const app = express();
const port = 9090; // 서버 포트

app.use(
  cors({
    origin: "http://localhost:3000",
    optionsSuccessStatus: 200,
    credentials: true
  })
);
app.use(express.json());
aapp.use(createMiddleware(...handlers));
app.listen(port, () => console.log(`Mock server is running on port: ${port}`));
```

<br>

#### **🗒️ src/mocks/handler.ts**

api 별로 어떤 요청에 어떤 응답을 줄지 세팅

```ts
import { http, HttpResponse, StrictResponse } from "msw";

const User = [
  { id: "gildong", nickname: "Gil dong" },
  { id: "cheolsu", nickname: "Cheol Su" },
  { id: "zoe", nickname: "Zoe" }
];

export const handlers = [
  http.post("/api/v1/login", () => {
    console.log("로그인");
    return HttpResponse.json(User[1], {
      headers: {
        "Set-Cookie": "connect.sid=msw-cookie;HttpOnly;Path=/"
      }
    });
  }),
  http.post("/api/v1/logout", () => {
    console.log("로그인");
    return HttpResponse.json(null, {
      headers: {
        "Set-Cookie": "connect.sid=;HttpOnly;Path=/;Max-Age=0"
      }
    });
  })
];
```

<br>

### **MSW 서버 실행**

package.json에 서버 실행 명령 스크립트를 등록합니다.  
watch 옵션으로 인해 서버 코드가 수정되면, 서버가 자동으로 재시작되기 때문에 유용하게 사용할 수 있습니다.  
(-> 서버 코드는 수정되면 재시작되어야 수정이 반영됩니다.)

```json
"scripts": {
  // ...
  "mock": "npx tsx watch ./src/mocks/http.ts"
}
```

```bash
$ npm run mock
# or
$ yarn mock
```

<br><br>

## **Next.js용 MSW 컴포넌트**

### **MSW 컴포넌트 생성**

Next.js에서 어떤 곳에서 MSW를 적용할지 분기 처리를 하기 위해서는 컴포넌트를 별도로 생성해주면 됩니다.

```ts
// src\app\_component\MSWComponent.tsx
"use client";
import { useEffect } from "react";

export const MSWComponent = () => {
  useEffect(() => {
    if (typeof window !== "undefined") {
      if (process.env.NEXT_PUBLIC_API_MOCKING === "enabled") {
        // NEXT_PUBLIC_API_MOCKING 환경 변수가 enabled일 때 MSW 실행
        require("@/mocks/browser");
      }
    }
  }, []);
};
```

> **MSW가 v2로 업그레이드되면서 if (typeof window !== 'undefined')로 감싸주게 바뀌었습니다.**
>
> window가 undefined가 아니다.  
> ⇒ window가 존재한다.  
> ⇒ 클라이언트 환경, 즉 브라우저이다.  
> ⇒ if문 안의 코드가 브라우저에서만 돌아가게끔 보장됩니다.

<br>

### **.env.local 파일 생성**

`.env` 파일에 환경 변수를 선언하게 되면 배포 환경에서도 해당 환경 변수가 적용됩니다.  
하지만, MSW는 개발 환경일 때만 사용하면 되므로 `.env.local` 파일에 환경 변수를 선언하게 되면 개발 환경일 때에만 해당 환경 변수가 유효합니다.

```
NEXT_PUBLIC_API_MOCKING = enabled
```

<br>

### **MSW 컴포넌트 적용**

```ts
// src\app\layout.tsx
export default function RootLayout({ children }: Props) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <MSWComponent />
        {children}
      </body>
    </html>
  );
}
```

<br><br>

## **MSW를 활용하는 방법**

MSW를 활용하면 단순한 API 응답 모킹뿐만 아니라, 다양한 네트워크 시나리오를 시뮬레이션할 수 있습니다.  
왜냐하면 MSW는 지연 응답, 네트워크 오류, 상태 코드 변화 등 다양한 네트워크 상황을 모킹할 수 있는 기능을 제공하기 때문입니다.  
이를 통해 실제 사용자가 겪을 수 있는 다양한 네트워크 환경을 테스트하고, 애플리케이션의 견고성을 높일 수 있습니다.

또한, MSW는 REST API뿐만 아니라 GraphQL API 모킹도 지원합니다.  
이는 API의 종류에 관계없이 MSW를 활용할 수 있음을 의미합니다.

Next.js는 서버와 클라이언트에서 동작하기 때문에, SSR 동작할 때에 서버에서도 MSW가 동작해야 합니다.
서버와 클라이언트 두 곳에서 MSW가 동작해야 하는데, 아직 서버에서 MSW를 동작시키는 방식이 나오지 않아서 매끄럽지 않습니다. 그래서 Node 서버를 활용하여 임시로 MSW를 동작시킵니다.

<br><br>

# **참고자료**

> [리액트에서 MSW(Mock Service Worker)를 활용한 API 모킹 전략](https://f-lab.kr/insight/using-msw-for-api-mocking-in-react)
>
> [MSW - 더 나이스한 목킹을 위한 고민](https://tech.madup.com/mock-service-worker/)
