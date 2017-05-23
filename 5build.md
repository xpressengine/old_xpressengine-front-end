# 5.Build
---
XE3 프론트엔드 최적화 및 번들링을 위해 gulp와 webpack을 사용하고 있습니다. `xpressengine/resources/assets`하위에 있는 코드들은 es2015, react, sass등이 사용되고 있으며 gulp와 webpack을 이용해 자바스크립트 transpiling 및 minimize, image최적화, css컴파일, 번들링 등을 하여 `xpressengine/assets` 하위 디렉토리에 복사합니다. XE3에서는 최적화된 코드를 로드하여 웹페이지 로딩시간을 개선 하였습니다. 

## Gulp
gulp관련 설정들은 `gulpfile.babel.js`에 정의되어 있고 `/resources/gulpTasks` 디렉토리에 css, image, settings, webpack 관련 task들을 분리하여 사용합니다.

### css.js
`css.js`에는 `resources/assets` 하위 디렉토리에 있는 sass파일들을 컴파일하는 테스크가 정의되어 있습니다.
> gulp assets:sass

### image.js
`image.js`에는 `resources/assets/core` 디렉토리 하위에 있는 이미지 파일들을 웹에 최적화 되도록 압축합니다. 이미지 파일 사이즈를 줄여 웹페이지 로드시간을 최소화합니다.
> gulp assets:image

### settings.js
`settings.js`에는 항상로드되어야 하는 자바스크립트 파일들을 번들링하고 `xpressengine/assets/core`하위로 최적화된 코드를 복사합니다. 
* clean:assets : `xpressengine/assets/core` 하위 디렉토리를 삭제합니다.

>gulp clean:assets

* copy:assets : `xpressengine/resources/assets/core`에 있는 파일들을 'xpressengine/assets/core'로 복사합니다.

>gulp copy:assets

* assets:chunk : 항상 로드되는 자바스크립트 파일들을 `xpressengine/assets/bundle.js` 파일로 번들링합니다. 

>gulp assets:chunk

* jscs : XE3 프론트엔드는 airbnb의 코딩컨벤션을 유지하고 있습니다. jscs 테스크는 airbnb의 코딩컨벤션에 준수하는 체크합니다.

>gulp jscs

### webpack.js
`webpack.js`에는 webpack설정을 읽어드려 실행하는 task가 있습니다.
> gulp webpack

## Webpack
webpack관련 설정은 `webpack.config.js`에 정의되어 있습니다. debug 모드로 빌드하게 될 경우에는 기본설정외에 `webpack.dev.config.js` 설정을 읽어드려 실행하고 production 모드로 빌드하게 될 경우에는 `webpack.prod.config.js`의 설정을 읽어드려 실행합니다.

## 프론트엔드 빌드 모드

### 개발 환경 빌드
개발 환경 모드로 빌드하게 되면 .map 파일을 생성하여 개발자도구에서 디버깅이 가능합니다.
> npm run dev

### 배포 환경 빌드
배포 환경 모드로 빌드하게 되면 js, css, image등을 최적화 합니다.
> npm run build