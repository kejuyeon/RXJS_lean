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
    <span>* city 예시 : London</span>
  </div>
  <div id="app-container">
    <div id="form">
      <label>city:</label>
      <input type="text" id="city-input">
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

```javascript
const appContainer = document.getElementById('app-container');
const cityInput = document.getElementById('city-input');
const addLocationBtn = document.getElementById('add-location');

const btnClickStream =
   Rx.Observable
    .fromEvent(addLocationBtn, 'click')
    .map(() => true)
    .forEach(val => { console.log('button click', val);});
        
```

`addLocationBtn`에 이벤트를 추가

콘솔이 찍히는걸 확인

<br/>
<br/>

```javascript
const cityInputStream =
      Rx.Observable
        .fromEvent(cityInput, 'input')
        .map(e => e.target.value)
        .filter(city => city.length === 6)
        .forEach(val => {console.log('input value', val);});
```
 input에 입력될때 6글자 이상일때 호출되도록 이벤트 추가
 
 콘솔 확인

<br/>
<br/>


```javascript
const cityStream =
    btnClickStream
      .withLatestFrom(cityInputStream, (click, city) => city)
      .distinct()
      .forEach(val => console.log('cityStream val', val));
```

> `distinct` 중복 입력된 값을 걸러줌

콘솔 확인

<br/>
<br/>

https://home.openweathermap.org/api_keys 의 api를 사용하여 날씨 정보를 가져옴

```javascript
  const getTemperature = city =>
    fetch(`http://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=APPID`)
      .then(res => res.json());
  const cityTemperatureStreamFactory = city =>
    Rx.Observable
      .fromPromise(getTemperature(city))
      .map(({ main: { temp } }) => ({ temp, city }));

    cityStream
      .flatMap(cityTemperatureStreamFactory)
      .forEach(({city, temp}) => {console.log(city, temp);});
```
콘솔 확인 날씨 정보가 딱
