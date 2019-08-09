# React 프로젝트 구성

### 1. VSC(Visual Studio Code) 개발 환경을 열어서 특정한 폴더(Folder)를 열어 줍니다.

- (이 때 가능하면, `관리자 권한`으로 개발환경을 열 수 있도록 합니다.)

### 2. yarn init 명령어를 통해 패키지(Package) JSON 파일을 생성합니다.

### 3. yarn add 명령어를 통해 리액트 라이브러리를 설치합니다.

```javascript
yarn add react react-dom
```

리액트 개발을 위하여 react와 react-dom이 모두 필요합니다.

### 4. yarn add 명령어를 통해 webpack을 설치합니다.

```javascript
yarn add --dev webpack webpack-dev-server
```
**webpack을 이용해 추후에 앱을 배포할 수 있어요.**    
또한 **webpack-dev-server를 이용해 실시간 로딩**으로 빠르게 개발할 수 있습니다.

### 5. yarn add 명령어를 통해 바벨(Babel)을 설치합니다.

```javascript
yarn add --dev babel-core babel-loader babel-preset-react-app
```

바벨 또한 개발 환경에서 필요하기 때문에 --dev 옵션으로 설치합니다.

### 6. yarn add 명령어를 통해 웹팩(Webpack) 클라이언트 모듈을 설치합니다.

```javascript
yarn add --dev webpack-cli
```

(--dev 혹은 -D라고 옵션을 붙여서 개발 종속성으로 설치합니다.)

<br/>

### 7. 소스코드를 작성하기 위해 다음과 같이 프로젝트를 구성합니다.

**public/index.html**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Word Cloud Project</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <meta name="theme-color" content="#E2E2E2">
  </head>
  <body>
    <div id="app"></div>
    <script type="text/javascript" src="main.js"></script>
  </body>
</html>
```

<br/>

**src/components/App.js**

```javascript
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <div>
        <h3>Hello World</h3>
      </div>
    );
  }
}

export default App;
```

<br/>

**src/main.js**

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';

ReactDOM.render(<App/>, document.getElementById('app'));
```

<br/>

**webpack.config.js**

```javascript
'use strict'
const path = require('path');

module.exports = {
  entry: {
    main: ['./src/main.js']
  },
  output: {
    path: path.resolve(__dirname, './build'),
    filename: '[name].js'
  },
  module: {
    rules: [{
      test: /\.js$/,
      include: path.resolve(__dirname, './src'),
      loaders: 'babel-loader'
    }]
  },
  plugins: [],
  devServer: {
    contentBase: './public',
      host: 'localhost',
      port: 8080
  }
}
```

<br/>

**.babelrc**

```javascript
{
  "presets": ["react-app"]
}
```

<br/>

**package.json**

```javascript
{
  "name": "wordcloud",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "dependencies": {
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
  },
  "scripts": {
    "start": "set NODE_ENV=development&&webpack-dev-server",
    "build": "set NODE_ENV=production&&webpack -p"
  },
  "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^8.0.6",
    "babel-preset-react-app": "^9.0.0",
    "webpack": "^4.38.0",
    "webpack-cli": "^3.3.6",
    "webpack-dev-server": "^3.7.2"
  }
}
```

맥의 경우 다음과 같다.

```javascript
"scripts": {
"start": "NODE_ENV=development webpack-dev-server",
"build": "NODE_ENV=production webpack -p"
},
```

<br/>

### 8. yarn start 명령어를 이용해 프로젝트를 동작시킵니다.

### 9. 구성된 프로젝트를 깃 허브(Git Hub)에 올리기

**.gitignore 파일 생성 및 소스코드 작성**   

```javascript
node_modules  
build
```

### 10. 터미널(Terminal)에서 Git 명령어로 소스코드 업로드
```javascript
// git 연동
git init

//전체 문서 git에 반영
git add .

//커밋
git commit -m "Intialize React Project"

//repository 연결
git remote add origin 깃주소복사

//repository 넣은 것 확인
git remote -v

//push 하기
git push --set-upstream origin master
```

<br/>

# material-ui 라이브러리

```javascript
yarn add @material-ui/core
yarn add @material-ui/icons
```

<br/>

# 파이어베이스로 리액트 프로젝트 배포

### 1. 빌드(Build)를 위한 웹팩 설정

```javascript
yarn add --dev copy-webpack-plugin
```

```javascript
'use strict'
const path = require('path');
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  entry: {
    main: ['./src/main.js']
  },
  output: {
    path: path.resolve(__dirname, './build'),
    filename: '[name].js'
  },
  module: {
    rules: [{
    test: /\.js$/,
      include: path.resolve(__dirname, './src'),
      loaders: 'babel-loader'
    }]
  },
  plugins: [
    new CopyWebpackPlugin([{
      context: './public',
      from: '*.*'
    }]),
  ],
  devServer: {
    contentBase: './public',
    host: 'localhost',
    port: 8080
  }
}
```

### 2. 각종 모듈 재설치

(필요할 시 수행하세요.)

```javascript
yarn add webpack-cli -D
```

```javascript
yarn add @material-ui/coure
```

### 3. 파이어베이스(Firebase) 패키지 설치 및 설정하기

```javascript
npm install -g firebase-tools
```
yarn add firebase-tools 명령으로 설치할 수 있습니다.  

이 때 firebase init 명령이 동작하지 않으면,   
관리자 권한으로 에디터를 실행하세요.   
또한 firebase 계정을 변경하고 싶을 때는   
firebase logout 및 firebase login 명령을 이용하시면 됩니다.

```javascript
firebase init
```

### 4. 기존의 build 폴더를 삭제한 뒤에 yarn build으로 재빌드하기

```javascript
yarn build
```

### 5. 파이어베이스 호스팅 서비스를 이용해 배포하기

```javascript
firebase deploy
```

### 6. .gitignore 파일 수정 및 푸시(Push)하기

```javascript
node_modules
build
.firebase/
firebase.json
.firebaserc
```

<br/>

# React에 웹 폰트(Web Font) 적용하기

### 1. Style 적용을 위한 라이브러리 추가하기

```javascript
yarn add style-loader
yarn add css-loader
```

### 2. 웹팩(Webpack) conf 파일 수정하기

```javascript
'use strict'
const path = require('path');
const CopyWebpackPlugin = require('copy-webpack-plugin');

module.exports = {
  entry: {
    main: ['./src/main.js']
  },
  output: {
    path: path.resolve(__dirname, './build'),
    filename: '[name].js'
  },
  module: {
    rules: [{
      test: /\.js$/,
      include: path.resolve(__dirname, './src'),
      loaders: 'babel-loader'
    }, {
      test: /\.css$/,
      loader: "style-loader!css-loader"
    }]
  },
  plugins: [
    new CopyWebpackPlugin([{
      context: './public',
      from: '*.*'
    }]),
  ],
  devServer: {
    contentBase: './public',
    host: 'localhost',
    port: 8080
  }
}
```

**./src/index.css**


```javascript
@import url(https://fonts.googleapis.com/earlyaccess/notosanskr.css);

div {
  font-family: 'Noto Sans KR' !important;
}
```

**./src/main.js**


```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './components/App';
import { MuiThemeProvider, createMuiTheme } from '@material-ui/core/styles';

const theme = createMuiTheme({
  typography: {
    useNextVariants: true,
    fontFamily: '"Noto Sans KR"'
  }
});

ReactDOM.render(
  <MuiThemeProvider theme={theme}>
    <App />
  </MuiThemeProvider>, 
  document.getElementById('app')
);
```

이후에 모든 컴포넌트 JS 파일에 import '../index.css';를 넣어주시면 됩니다.


