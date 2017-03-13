# 3.1 Lightbox
---

이미지 요소들을 보여주는 Viewer를 생성합니다. 좌, 우 슬라이드 기능 및 닫기 버튼을 기본 제공합니다. (Desktop, Mobile 지원)

## $(selector).lightbox()

```html
<div class="images" data-toggle="xe-lightbox" data-selector="img">
   <img src="sample/img/@sample_img.jpg">
   <img src="sample/img/@sample_img2.jpg">
   <img src="sample/img/@sample_img3.jpg">
   <img src="sample/img/@sample_img4.jpg">
   <img src="sample/img/@sample_img5.jpg">
   <img src="sample/img/@sample_img6.jpg">
   <img src="sample/img/@sample_img7.jpg">
</div>
```
```javascript
$('.images > img').lightbox();
```


