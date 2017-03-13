#4.2 Utils.isImage( mimeType )
---
mime type으로 웹용 이미지 타입인지 확인하여 true, false를 리턴해줍니다.
## arguments
### mimeType (string)
- image/jpg
- image/jpeg
- image/png
- image/gif

```javascript
Utils.isImage('image/jpg') // true
Utils.isImage('image/bmp') // false
```