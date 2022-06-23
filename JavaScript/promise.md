# Promise
자바스크립트 비동기 처리에 사용되는 객체

<br>

### 사용 이유
>비동기 처리의 경우 특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 특성이 있기 때문에 받아온 데이터를 처리해야 할 경우 콜백함수를 사용한다. 이때 콜백 함수를 중첩하여 사용할 경우 콜백 지옥에 빠지게 된다. 이러한 문제를 해결하기 위해 Promise를 사용하게 된다.

<br>

### 코드

```javascript
// 콜백함수 사용
function getData(callbackFunc) {
  $.get('url 주소/products/1', function(response) {
    callbackFunc(response); 
  });
}

getData(function(tableData) {
  console.log(tableData);
});

// 프로미스 적용
function getData(callback) {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      resolve(response);
    });
  });
}

getData().then(function(tableData) {
	  console.log(tableData); 
}).catch(function(err) {
	console.log(err);
});
```

<br>

### 3가지 상태
#### Pending(대기)
비동기 처리 로직이 아직 완료되지 않은 상태

#### Fulfilled(이행)
비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태

#### Rejected(실패)
비동기 처리가 실패하거나 오류가 발생한 상태
