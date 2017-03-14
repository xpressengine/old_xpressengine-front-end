# 5.Build
---
프론트엔드 관리 환경을 최적화 하고 자동화하기 위해 Gulp와 Webpack 빌드 도구를 통해 빌드 관리를 하고 있습니다. 우선 **빌드를 하게 되면 XE에 개발된 프론트엔드 부분(Core)이 초기화** 되기 때문에 XE프론트엔드 Core부분이 커스터마이징되어 있는 경우라면 실행하지 않는 것을 추천드립니다.
빌드를 할 경우 XE3가 설치된 디렉토리 **/xpressengine** 하위 디렉토리인 ```/xpressengine/resources/assets``` 디렉토리에 정의되어 있는 js, css, jsx, sass 등의 코드들이 정의된 설정에 따라 ```/xpressengine/assets``` 하위로 이동되어 집니다. 즉 **/xpressengine/resources/assets** 하위의 코드들은 XE프론트엔드 코드들의 **원본**이며 **/xpressengine/assets** 하위의 코드들이 빌드되어져 사용되는 소스코드입니다.

