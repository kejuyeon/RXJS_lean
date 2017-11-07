## 반응형 프로그래밍 RxJS

RxJS는 이벤트 스트림과 데이터를 쉽게 만들고 다룰 수 있도록 도우는 라이브러리다. 복잡하지만 가독성이 좋은 비동기적 코드를 더 쉽게 작성할 수 있도록 도운다.




## 예제

### 기본 설정

```html
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>날씨검색</title>
  <style>
    body {
      font-family: NanumGothic, AppleGothic, Myriad Pro, MalgunGothic, Arial;
       margin: 20px;
    }
    .example {
      padding: 10px 0;
    }
    .location-wather {
      float: left;
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 4px;
      margin: 10px;
      text-align: center;
    }
    #add-location {
      border: 1px solid #e8e8e8;
      background-color: #fff;
      color: #494949;
      font-size: 15px;
      padding: 5px;
      border-radius: 4px;
    }
    input {
      font-size: 12px;
      padding: 5px;
    }
    #add-location:hover {
      border: 1px solid #d4bd93;
      background-color: #fde2b0;
      color: #000;
      font-size: 15px;
      padding: 5px;
      border-radius: 4px;
    }
  </style>
</head>
<body>
  <div class="example">
    <span>* zipcod 예시 : us 마운틴뷰 94040</span>
  </div>
  <div id="app-container">
    <div id="form">
      <label>Zip Code:</label>
      <input type="text" id="zipcode-input">
      <button id="add-location">Add Location</button>
    </div>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/rxjs/4.1.0/rx.all.min.js"></script>
  
  <script>
    console.log('RxJS ?', !!Rx);
  </script>
  </body>
</html>
```

콘솔에 `true`가 나오면 설정끗!

### Script 작성


