# 1.3 XE.Request

## XE.Request.get( url [, data] [, callback] [, dataType] )
서버로부터 데이터를 전달 받습니다.
### url (string)
요청보낼 URL 값
### data (object or string)
서버로 전송할 파라미터
### callback (function)
요청 성공시 실행될 콜백
### dataType (string)
서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)

```javascript
XE.Request.get('/item/3', function(data) {
      console.log(data);
});
```

## XE.Request.post( url [, data] [, callback] [, dataType] )
### url (string)
요청보낼 URL 값
### data (object or string)
서버로 전송할 파라미터
### callback (function)
요청 성공시 실행될 콜백
### dataType (string)
서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)
```javascript
XE.Request.post('/item', {name: 'xe'},  function(data) {
      console.log(data);
}, 'json');
```
  
## XE.ajax( url [, settings] ) or XE.ajax( [settings] )
XE.ajax는 jQeury의 $.ajax를 wrapping한 형태를 취하고 있습니다. settings에 사용되는 옵션들은 jQuery의 옵션들을 그대로 사용하실 수 있습니다.
### url (string)
요청보낼 URL 값
### settings (object)
* type (string) http method 'get' | 'post' 등
* data (object) 서버로 전송할 파라미터
* dataType (string) 서버로부터 전송되는 데이터의 타입 (json, xml, html, text, script)
* success (function) 요청 성공시 실행될 콜백
* error (function) 요청 실패시 실행될 콜백

```javascript
XE.ajax('/item', {
      type: 'get',
      dataType: 'json',
      data: {
        id: 'p3'
      },
      success: function(data) {
        console.log(data);
      },
      error: function(jqXHR, textStatus, errorThrown) {
        console.log(jqXHR, textStatus, errorThrown);
      }
});
```

