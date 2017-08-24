# 3.7 XeInfinite
---
XeInfinite는 slick grid 라이브러리를 wrapping한 오브젝트이며 UI상의 row의 갯수가 많아 질 경우 스크롤시 일정한 갯수의 DOM을 재사용함으로써 UI를 최적화합니다. slick grid에 대한 자세한 API레퍼런스는 아래의 링크를 통해 참조하실수 있습니다.

SlickGrid Github - https://github.com/mleibman/SlickGrid
SlickGrid API Reference - https://github.com/mleibman/SlickGrid/wiki/API-Reference

XeInfinite 기능을 사용하기 위해서는 `assets/core/xe-ui-component/xe-infinite.js`를 로드하여야 합니다.

## XeInfinite.init(options, customOptions)
XeInfinite를 초기화합니다. 필요한 라이브러리를 로드하고 데이터 요청, 이벤트 핸들러를 바인딩합니다.

### options
#### wrapper (string) 
XeInfinite를 나타낼 상위 요소 셀럭터를 나타냅니다.
#### template (string)
반복될 template 문자열 형태로 나타냅니다. 템플릿의 사용되는 변수들은 options의 data 오브젝트의 property와 맵핑되어 치환됩니다.
#### data (array< object >)
template에 사용될 초기 데이터를 나타냅니다. object로 구성된 리스트를 사용합니다.
#### loadRowCount (number)
onGetRows를 호출하기전 체크. 스크롤시 남아있는 row의 갯수. loadRowCount갯수만큼 스크롤이 남을 경우 onGetRows를 호출한다.
#### rowHeight (number)
스크롤되는 화면의 row의 높이값을 나타냅니다. 기본값으로 25를 사용하며 25px로 적용됩니다.
#### onGetRows (function)
스크롤중 데이터를 요청해야 할 경우 호출될 메소드. 




