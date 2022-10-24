# Bundler
## 1. 번들러란?
이번에는 번들러(Bundler)에 대해 알아보는 시간을 가져봅시다. 지금까지 parcel 번들러를 사용해왔으며 이외에도 webpack, rollup 등의 여러 종류가 있습니다. 특히, webpack 번들러가 많이 사용되고 있습니다.

## 2. 번들러의 개념
실제로 웹사이트에서는 HTML, CSS, JavaScript가 동작을 합니다. 그러나 순수하게 3가지만을 사용하여 코딩을 하기엔 비효율적이라 할 수 있습니다.

그렇기 때문에 SCSS, React, TypeScript 등의 여러 라이브러리나 프레임워크를 사용하여 코딩을 진행하고 프로젝트를 제작합니다. 그리고 이들을 번들러를 통해 변환하는 과정을 거쳐 HTMl, CSS, JavaScript로 웹에서 동작시킬 수 있도록 합니다.
물론, 번들러가 직접적으로 변환시키는 것은 아닙니다. 예를 들어, SCSS 문법을 CSS로 변환시킬 때 parcel-bundler가 Sass라는 외부 패키지를 설치하여 이로부터 도움을 받아 완료한 것입니다.

## 3. parcel VS webpack
### 3.1 parcel
parcel 번들러는 별도의 구성이 없는 단순한 자동 번들링을 제공해줍니다. 그러므로 매우 편리한 번들러라고 할 수 있습니다. 그러나 webpack 번들러에 비해 구성이 꼼꼼하지 않습니다. 그러므로 프로젝트의 규모가 커질수록 parcel 번들러의 아쉬움을 발견하는 경우가 있습니다. 이러한 이유로 parcel 번들러는 소/중형 프로젝트에 적합하다고 할 수 있습니다.

### 3.2 webpack
webpack 번들러는 매우 꼼꼼하고 자세하게 번들링할 수 있는 구성 옵션을 설정해줄 수 있습니다. 그러한 구성 옵션을 통해 개발자의 입맛에 맞게 정리를 할 수 있습니다. 그러므로 당연하게도 중/대형 프로젝트에 유용하게 사용 가능합니다. 그러나 아무래도 이러한 이유로 확인해야할 사항이 많다는 단점이 있습니다.

# 프로젝트 생성
## 1. Start the project
parcel-bundler에 대해 잘 학습할 수 있도록 하기 위해 실제로 프로젝트를 생성해줍니다.

### 1.1 패키지 설치
npm을 통해 package.json 파일을 생성하고 parcel-bundler를 설치해줍니다.
```bash
$ npm init -y

$ npm i -D parcel-bundler
```

### 1.2 package-json 파일
package-json 파일을 오픈하여 script 내에 아래와 같이 parcel 번들러를 이용하여 개발을 할 수 있도록 합니다.
```script
"scripts": {
    "dev": "parcel index.html",
    "build": "parcel build index.html"
  },
```
### 1.3 index.html
index.html 파일과 main.scss, main.js 파일을 연결시켜줍니다. 그리고 CSS를 초기화시켜주기 위해 reset css mdn으로 구글 검색하여 나온 아래 링크를 SCSS 링크 태그 위에 코딩해줍니다.
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Parcel Bundler</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reset-css@5.0.1/reset.min.css">
  <link rel="stylesheet" href="./scss/main.scss">
  <script defer src="./js/main.js"></script>
</head>
<body>
  <h1>Hello Parcel!!</h1>
</body>
</html>
```

### 1.4 개발 서버 오픈
npm을 통해 개발 서버를 오픈해줍니다.
```bash
$ npm run dev
```

# 정적 파일 연결
본인이 프로젝트에 연결되었으면 하는 파일을 개발 서버를 열거나 제품화 시킬 때, 직접 웹페이지에 연결되는 dist 폴더로 자동으로 넣어줄 수 있는 패키지에 대해 배워봅시다.

이를 정적 파일 연결이라하며, 새로운 개념이므로 아래 내용으로 살펴보도록 합시다.

## 1. favicon.ico
프로젝트 내에 favicon.ico 파일을 준비해줍니다. 어떤 파일이건 상관없으며, 저는 flaticon 홈페이지의 아래 파일을 이용하여 진행하도록 하겠습니다.

[img -> ico 파일로 변환](https://www.icoconverter.com/)

![image](https://user-images.githubusercontent.com/114347341/197557525-9cd7328f-be46-4b50-b088-6e06dd60aa56.png)


## 2. 연결 오류
프로젝트 내에 favicon.ico 파일을 넣어놨으나 파비콘이 웹페이지에 구현되지 않음을 확인할 수 있습니다. 이는 index.html 파일이 parcel-bundler를 통해 dist란 폴더로 변환되어 삽입되었기 때문입니다.

## 3. dist
dist 폴더 내의 index.html 파일을 열면, 아래의 모습처럼 연결된 CSS, JavaScript, img 파일 등이 앞에 기호가 붙어 새롭게 연결되어 있음을 볼 수 있습니다.

이처럼 웹에서 확인하는 index.html 파일은 dist 폴더 내에 있는 파일이라고 보시면 됩니다.

![image](https://user-images.githubusercontent.com/114347341/197557426-93ac57e9-8d8f-45a8-b22a-1bb3d76b0343.png)

## 4. static files copy
구글에 parcel plugin static files copy를 검색하거나 아래 링크로 들어가시면 됩니다. 설치하는 방법과 예시를 통해 해당 패키지를 사용하는 방법에 대해 확인할 수 있습니다.

## 5. 정적 파일 연결
실제로 정적 파일 연결을 위한 터미널 명령어와 설정 방법에 대해 알아봅시다.

### 5.1 패키지 설치
정적 파일 연결 패키지를 개발용으로 설치해줍니다.
```bash
npm install -D parcel-plugin-static-files-copy
```

### 5.2 package.json
package.json 파일에 아래와 같이 코딩을 진행해줍니다.이는 설치한 패키지가 static이라는 폴더를 dist 폴더로 복사 및 붙여넣기를 해주는 개념입니다.
```json
"staticFiles": {
    "staticPath": "static"
}
```
### 5.3 static 폴더 생성
위 코딩 내용에 따라 프로젝트 내에 static 폴더를 생성해주도록 합니다. 그리고 favicon.ico 파일을 해당 폴더에 넣어줍니다.

npm run dev로 개발 서버를 열고 확인하면, static 폴더로 파비콘 파일이 옮겨져있으며 아래와 같이 연결이 잘 되었음을 볼 수 있습니다.
![image](https://user-images.githubusercontent.com/114347341/197558159-a70c2f4c-cc38-44a7-aa59-7a6088d748dd.png)

# autoprefixer
웹페이지 내에서 개발자 도구로 확인할 때, display: webkit-box등과 같이 코딩을 진행한 적이 없는 내용이 포함되어 있는 것을 볼 수 있습니다.

이는 웹 표준이 권고안으로 나오기 전에 브라우저를 제작하는 벤더사인 예를 들면 크롬을 제작하는 구글, 인터넷 익스플로러를 제작하는 마이크로소프트 회사에서 미리 본인들의 브라우저 내에서 동작할 수 있는 구조를 만들어 놓습니다. 시험적인 기능을 적용하는 것이라 생각하시면 됩니다.

그러나 해당 기능은 표준 기술이 아니므로 webkit이나 ms라는 접두사를 붙여 사용합니다. 이렇게 여러 브라우저의 종류나 버전에 따라 기능의 사용 여부가 달라지기 때문에 이를 확인할 수 있는 것입니다.

결국, 비교적 신기술이 구현되지 않는 구형의 브라우저에서도 최신의 CSS 기술이 동작할 수 있도록 일종의 보험을 들어두는 것이 webkit이나 ms로 시작하는 공급 업체 접두사(Vendor Prefix)를 적용하는 방식입니다.

이러한 공급업체 접두사를 각 속성별로 모두 외워 사용하는 것은 거의 불가능하기에 이를 자동으로 진행해주는 패키지가 autoprefixer이며, 이를 설치하는 방법에 대해 알아봅시다.

## autoprefixer 설치 및 설정
### 1.1 패키지 설치
postcss와 autoprefixer 두 가지 패키지를 개발용으로 설치해줍니다.
```bash
npm i -D postcss autoprefixer
```
### 1.2 package.json
package.json 파일에 browerslist 옵션을 코딩해줍니다. browerslist 옵션은 현재 NPM 프로젝트에서 지원할 브라우저의 범위를 명시하는 용도입니다.
```json
"browserslist": [
    "> 1%",
    "last 2 versions"
  ]
```
이것은 현재 프로젝트에서 전 세계의 점유율이 1% 이상인 모든 브라우저의 마지막 2개 버전까지 모두 지원을 하겠다는 의미입니다.

![image](https://user-images.githubusercontent.com/114347341/197558721-13f3d590-6668-468c-b550-a7594a64dd81.png)

### 1.3 .postcssrc.js 파일 생성
.postcssrc.js 마침표로 시작하는 rc(runtime configuration) 파일, 즉 구성 파일을 만들어줍니다. 마침표로 시작하는 것은 구성 옵션이나 숨김 파일을 의미합니다.

### 1.4 import & export

.postcssrc.js 파일 내에 아래 내용을 코딩해줍니다.

```script
const autoprefixer = require('autoprefixer')

module.exports = {
  plugins: [
    autoprefixer
  ]
}
```
주로 사용하는 import, export 키워드는 node.js 환경에서 사용이 불가하여 CommonJS 방식인require(), module exports 키워드를 이용하여 JavaScript 파일을 가져오고 내보냅니다.

![image](https://user-images.githubusercontent.com/114347341/197558813-b7c7a235-9cb7-4ce3-af83-dcbf9d537470.png)

### 1.5 autoprefixer 버전 다운그레이드
PostCSS plugin autoprefixer requires PostCSS 8.
위의 모든 단계를 완료하고 개발 서버를 오픈하려하면 위와 같이 에러 메시지가 발생하게 됩니다. 이는 autoprefixer와 PostCSS의 버전이 충돌하고 있기 때문입니다.

이러한 이유로 10버전인 autoprefixer의 9버전으로 다운그레이드 해줍니다.

```bash
npm i -D autoprefixer@9
```

![image](https://user-images.githubusercontent.com/114347341/197558967-dc22022e-8758-48ce-9ce6-fdcb9a21dedf.png)

### 1.6 개발 서버 오픈
개발 서버를 열어서 패키지가 잘 설치되었는지 확인해줍니다. 확인을 위한 간단한 방법은 CSS 파일 내 한 요소에 display: flex로 설정하고 아래와 같이 명시되어 있다면, 성공적으로 설치되었음을 알 수 있습니다.

![image](https://user-images.githubusercontent.com/114347341/197559069-11c03c89-905c-4029-8355-eb0f004ce36a.png)

# Babel
Babel은 ECMAScript 2015+ 코드를 이전 JavaScript 엔진에서 실행할 수 있는 이전 버전과 호환되는 JavaScript 버전으로 변환하는 데 주로 사용되는 무료 오픈 소스 JavaScript 트랜스 컴파일러입니다.
출처: Babel 위키백과

# ECMAScript
Babel을 쉽게 이해하기 위해서는 모두 아시다시피 ECMAScript, ES에 대해 알아야합니다. JavaScript의 표준을 ECMAScript라 부르며, 2015년 ES는 새로운 버전이 출시되었고 그것이 ES6입니다. 그리고 최신의 JavaScript 문법으로 사용하는 것들은 ES6를 포함한 ES7, ES8입니다.

# Compiler
그러나 ES6 이상의 최신의 문법이 작동하지 않는 구형의 브라우저에서는 서비스가 원활히 동작하지 않습니다. 이러한 최신의 문법으로 작성한 JavaScript 코드를 Babel을 통해 이러한 브라우저들에서도 동작할 수 있는 ES5 버전으로 변환을 해줄 수 있고, 이를 '컴파일'한다고 합니다. 그리고 이러한 기능을 하는 Babel을 '컴파일러'라고 부릅니다.

# Babel 설치 및 설정
## 1.1 패키지 설치
babel/core를 포함한 3가지 패키지를 개발 의존성 모듈로 설치해줍니다.
```bash
npm i -D @babel/core @babel/preset-env @babel/plugin-transform-runtime
```
## 1.2 package.json
package.json 파일에 browerslist 옵션을 코딩해줍니다. browerslist 옵션은 현재 NPM 프로젝트에서 지원할 브라우저의 범위를 명시하는 용도입니다.
```json
"browserslist": [
    "> 1%",
    "last 2 versions"
  ]
```
이것은 현재 프로젝트에서 전 세계의 점유율이 1% 이상인 모든 브라우저의 마지막 2개 버전까지 모두 지원을 하겠다는 의미입니다.

## 1.3 .babelrc.js 파일 생성
.babelrc.js 마침표로 시작하는 rc(runtime configuration) 파일, 즉 구성 파일을 만들어줍니다. 마침표로 시작하는 것은 구성 옵션이나 숨김 파일을 의미합니다.

## 1.4 export
.babelrc.js 파일 내에 아래 내용을 코딩해줍니다.
```script
module.exports = {
  presets: ['@babel/preset-env'],
  plugins: [
    ['@babel/plugin-transform-runtime']
  ]
}
```
위 작업으로 프로젝트에서 작성하는 모든 JavaScript는 Babel을 통해 ES5 버전으로 변환되어 브라우저에서 동작하게 됩니다.

![image](https://user-images.githubusercontent.com/114347341/197559577-250b838c-c990-4018-acc8-cc1fca1c5f43.png)

## 1.5 개발 서버 오픈
개발 서버를 열어서 패키지가 잘 설치되었는지 확인해줍니다. 확인을 위한 간단한 방법으로 main.js 파일에 아래와 같이 비동기 함수를 작성합니다.
```script
async function test() {
  const promise = Promise.reseolve(123)
  console.log(await promise)
}
test()
```
Babel이 정상적으로 작동했다면, 아래 그림과 같이 콘솔창에 123이 출력된 것을 볼 수 있습니다.

![image](https://user-images.githubusercontent.com/114347341/197559718-a7eb3c2c-b820-4be9-9c60-0e75ff13c5d0.png)

# 커맨드 라인 인터페이스(CLI)
명령 줄 인터페이스 CLI, 커맨드 라인 인터페이스 또는 명령어 인터페이스는 가상 터미널 또는 텍스트 터미널을 통해 사용자와 컴퓨터가 상호 작용하는 방식을 뜻한다.
출처: CLI 위키백과

[parcel한국어판](https://ko.parceljs.org/cli.html)

Parcel-bundler CLI
Parcel-bundler에서 사용하는 여러 CLI에 대해 알아보는 시간을 가져봅시다.

## 1. Serve
개발용 서버를 시작하는 명령어입니다.

$ parcel index.html

## 2. Build
assets을 빌드합니다. 제품화하는 과정에서 필요한 명령어입니다.

$ parcel build index.html

![image](https://user-images.githubusercontent.com/114347341/197560873-af312266-8e62-4e9c-aef5-4894f2dbc04c.png)

# 옵션
package.json 파일의 옵션을 변경하는 명령어입니다.

## 1. 결과물 디렉토리
기본값은 dist이며, 다른 폴더명으로 변경을 원할 때 사용하는 명령어입니다.

```bash
$ parcel build entry.js --out-dir build/output

혹은

$ parcel build entry.js -d build/output
```

## 2. 포트 번호
기본값은 1234이며, 개발 서버 오픈 시에 포트 번호를 변경할 때 사용하는 명령어입니다.

```json
 "scripts": {
    "dev": "parcel index.html --port 1216",
    "bulid": "parcel build index.html"
  },
```
혹은
```bash
$ parcel serve index.html --port 1216
```

![image](https://user-images.githubusercontent.com/114347341/197560718-53a21347-17c8-4bfb-879f-03e6164e844b.png)

![image](https://user-images.githubusercontent.com/114347341/197560137-7d486acc-7cc8-4c0e-b313-b108becaa42a.png)


## 3. 브라우저에서 열기
기본값은 비활성이며, 아래 명령어를 통해 개발 서버를 오픈하게 되면 자동으로 브라우저에 연결되게 됩니다.

```bash
$ parcel index.html --open
```

## 4. 빠른 모듈 교체 비활성화
기본값은 HMR 활성이며, 이는 Hot Module Replacement의 약자로 런타임에 페이지 새로고침 없이 수정된 내용을 자동으로 갱신하는 방식이며 이를 활성화한다는 의미입니다. 아래 명령어를 통해 이를 비활성화할 수 있습니다.

```bash
parcel index.html --no-hmr
```

## 5. 파일시스템 캐시 비활성화
기본값은 캐시 활성이며, 이는 개발 서버를 오픈하거나 제품화를 할 때 캐시가 활성화 되어있어 더 빠르게 내용이 처리될 수 있습니다. 그러나 이러한 경우 때때로 문제가 발생하는 상황도 있으므로 필요에 따라 아래 명령어를 통해 비활성화할 수 있습니다.

```bash
parcel build entry.js --no-cache
```



















































































