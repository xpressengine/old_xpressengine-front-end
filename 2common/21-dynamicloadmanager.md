### dynamicLoadManager
DynamicLoadManager는 script, css파일등을 비동기로 로드하고 스크립트 중복 로드를 방지합니다.

# 2.1 DynamicLoadManager
## DynamicLoadManager.jsLaod( url [, load] [, error] )
javascript파일을 로드하고 요청 성공시 load콜백을 실행합니다.
##### url (string)
로드할 스크립트의 url주소
##### load (function)
로드 성공시 호출될 콜백
##### error (function)
로드 실패시 호출될 콜백
```javascript
DynamicLoadManager.jsLoad('assets/common/utils.js', function() {
    console.log('loaded');
}, function() {
    console.error('load error!');
});
```

#### DynamicLoadManager.jsLoadMultiple( url[] [, callbackObj] )
여러개의 javascript파일을 순차적으로 로드하고 요청 성공시 각각 load콜백을 실행합니다. 모든 파일이 로드되면 complete를 호출합니다.
##### url (string)
##### callbackObj (object)
* load (function)
* error (function)
* complete (function)

```javascript
DynamicLoadManager.jsLoadMultiple([
    '/assets/test/test1.js',
    '/assets/test/test2.js',
    '/assets/test/test3.js',
    '/assets/test/test4.js',
    '/assets/test/test5.js'
], {
    load: function() {
      console.log('loaded');
    },
    error: function() {
      console.log('error');
    },
    complete: function() {
      console.log('complete');
    }
});
```

#### DynamicLoadManager.cssLoad( url [, load] [, error] )
css파일을 로드하고 요청 성공시 load콜백을 실행합니다.
##### url (string)
로드할 스크립트의 url주소
##### load (function)
로드 성공시 호출될 콜백
##### error (function)
로드 실패시 호출될 콜백
```javascript
DynamicLoadManager.cssLoad('/assets/test/test.css', function() {
  console.log('loaded');
});
```
