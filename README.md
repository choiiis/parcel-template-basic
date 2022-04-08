## Parcel Template

parcel 기본 템플릿 업로드용  
(FastCampus FE 강의 中 Parcel Bundler 실습)

### Parcel bunlder 패키지 설치

```bash
npm i parcel-bundler -D
```

### Static files 연결 (favicon 적용)

favicon을 dist로 자동으로 넣기

- Ico Converter 이용해서 favicon 생성 - 32 pixel 충분
- 패키지 install

```bash
npm i -D parcel-plugin-static-files-copy
```

- package.json 수정

```json
"devDependencies": {
  "parcel-bundler": "^1.12.5",
  "parcel-plugin-static-files-copy": "^2.6.0",
  "sass": "^1.50.0"
},
"staticFiles": {
  "staticPath": "static"
}
```

- static 디렉토리 생성 -> 하위에 favicon.ico 이동
- npm run dev 하면 dist 하위에 favicon.ico 자동 생성

### Autoprefixer

표준 기술이 돌아가지 않는 경우 동작하도록 함 (Vendor Prefix)  
스타일 보험 형태로 사용한다고 볼 수 있음

- postcss, autoprefixer 2개 패키지 설치

```bash
npm i -D postcss autoprefixer
```

- browserslist 옵션 추가 : npm 프로젝트에서 지원할 브라우저 범위 명시.

```json
"browswerslist": [
  "> 1%",
  "last 2 versions"
]
```

점유율이 1% 이상인 브라우저의 최신 2개 버전까지 지원한다는 뜻

- .postcssrc.js 파일 생성 \*뒤에 rc(runtime configuration) 붙은 파일은 구성 파일을 의미

```js
module.exports = {
  plugins: [require("autoprefixer")],
};
```

\*\* version 오류 발생할 경우 downgrade

```bash
npm i -D autoprefixer@9
```

### Babel

Javascript ES6, ES7, ES8, ... 등 최신 버전이 동적하지 않는 구형 브라우저에서 JS가 돌아갈 수 있도록 ES5로 컴파일 하는 도구. 즉, Babel은 컴파일러

- 패키지 install

```bash
npm i -D @babel/core @babel/preset-env
```

- .babelrc.js 생성

```js
module.exports = {
  presets: ["@babel/preset-env"],
};
```

- async, await 사용하기

```js
console.log("Hello Parcel!");

async function test() {
  const promise = Promise.resolve(123);
  console.log(await promise);
}

test();
```

에러가 남 - @babel/plugin-transform-runtime 패키지 필요

```bash
npm i -D @babel/plugin-transform-runtime
```

.babelrc.js 수정

```js
module.exports = {
  presets: ["@babel/preset-env"],
  plugins: [["@babel/plugin-transform-runtime"]],
};
```
