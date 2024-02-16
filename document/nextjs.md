# NextJS 개념

## 프로젝트 생성
```bash
npx create-next-app my-app
```

## 기본 폴더 구조
```bash
├─app # 루트 폴더
│  ├─dashboard
│  │  ├─customers
│  │  └─invoices
│  ├─lib
│  └─ui
├─node_modules # 필요한 모듈
└─public # 정적 파일
``` 

## 라우팅
파일 시스템 라우팅
![Alt text](./image/image1.png)

## UI
layout.tsx 및 page.tsx 파일을 사용하여 각 경로에 대해 별도의 UI를 만들 수 있음.
![Alt text](./image/image2.png)
- page.tsx - 해당 파일 경로에 대한 UI
- layout.tsx - 여러 페이지 간 공유되는 UI
![Alt text](./image/image3.png)
- 부분 렌더링 기능 - 레이아웃은 렌더링 X, 페이지는 렌더링 O

## 페이지 탐색
- `<Link>` - 페이지 간 연결 <br />
    `<Link>` 태그를 사용하면 NextJS가 백그라운드에서 연결된 경로에 대한 코드를 미리 가져옴

## use server && use client
| | Server Component | Client Component |
|-|-|-|
| 데이터 가져오기| ✅  | ⚠️ |
| 백엔드 리소스에 직접 액세스하기 | ✅ | ❌ |
| 서버에 민감한 정보 유지하기 | ✅  | ❌ |
| 큰 종속성을 서버에 유지/클라이언트 측 JavaScript 줄이기 | ✅ | ❌ |
| 상호 작용 및 이벤트 리스너 추가하기(onClick, onChange 등)	 | ❌ | ✅ |
| 상태 및 라이프사이클 효과 사용하기(useState, useReducer, useEffect 등) | ❌ | ✅ |
| 브라우저 전용 API 사용하기 | ❌ | ✅ |
| 상태, 효과 또는 브라우저 전용 API에 의존하는 사용자 지정 훅 사용하기 | ❌ | ✅ |
| React Class 컴포넌트 사용하기 | ❌ | ✅ |


## 정적 렌더링
- 데이터 가져오기 및 렌더링이 서버에서 발생
- 사용자가 애플리케이션을 방문할 때마다 캐시된 결과가 제공
- ex) 블로그 같이 내용이 변하지 않는 것에 사용

## 동적 렌더링
- 각 사용자의 콘텐츠가 서버에서 렌더링 됨
- ex) 대시보드같이 개인화된 콘텐츠를 제공하는 것에 사용 

## 로그인
### NextAuthJS
```bash
npm install next-auth@beta
```
- 애플리케이션에 대한 비밀 키 생성 - .env 파일에서 AUTH_SECRET에 추가
```bash
openssl rand -base64 32
```
#### auth.config.ts
- NextAuthJS에 대한 구성 옵션
- 경로 보호 - 미들웨어를 사용하여 사용자가 로그인하지 않으면 페이지 엑세스 X
#### auth.ts
- 비밀번호 해싱
- 로그인 기능
#### middleware.ts
- 인증 확인 - 인증이 확인될 때까지 보호된 경로 렌더링 X