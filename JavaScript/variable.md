# var, let, const 차이점

### 차이점

1.  **중복선언** 가능 여부

2.  **재할당**  가능 여부

3. 변수  **스코프** 유효범위

4. 변수  **호이스팅** 방식

5.  **전역객체 프로퍼티**  여부
<br/>

## 중복선언
|var|let|const|
|-|-|-|
|가능|불가능|불가능|


```JavaScript
// var
var a = 30;
console.log(a);	// 30
 
var a = 20;
console.log(a);	// 20

//let
let a= 20;
console.log(a);	


let a = 30;		// SyntaxError: Identifier 'a' has already been declared
console.log(a);

// const
const a= 20;
const a = 30;	// SyntaxError: Identifier 'a' has already been declared
```

 - var의 경우 마지막에 선언한 변수의 초기화 값이 출력됨.
 - let과 const의 경우 에러가 발생하여 출력되지 않음.

<br/>

## 재할당
|var|let|const|
|-|-|-|
|가능|가능|불가능|

```javaScript
// var
var a = 10;
console.log(a);	// 10
a = 20;
console.log(a);	// 20

// let 
let b = 10;
console.log(b);	//10
b = 20;
console.log(b);	//20
 
// const
const c = 10;
console.log(c);	//10
c = 20;	// TypeError: Assignment to constant variable.
```
- const의 경우 처음 선언할 때 반드시 초기화를 해주어야함.
<br/>

## 스코프(Scope)
유효한 참조 범위
|var|let|const|
|-|-|-|
|함수 레벨 스코프|블록 레벨 스코프|블록 레벨 스코프|

```javaScript
// var
function fnTest(){
	var a = 10;
	console.log(a);	
}

fnTest();		// 10
console.log(a);	// ReferenceError: a is not defined
	
if(true) {
	var b = 20;
}
console.log(b);	// 20
 
// let 
function fnTest(){
	let a = 10;
	console.log(a);
}

fnTest();
console.log(a);	// ReferenceError: a is not defined
	
if(true) {
	let b = 20;
}
console.log(b);	// ReferenceError: b is not defined
 
// const 
function fnTest(){
	const a = 10;
	console.log(a);
}

fnTest();
console.log(a);	// ReferenceError: a is not defined
	
if(true) {
	const b = 20;
}
console.log(b);	// ReferenceError: b is not defined
```
- var의 경우 함수 내부에 선언된 변수는 함수 내부에서만 참조가 가능하고 외부에서 참조할 경우 에러가 발생

- 또한, 함수가 아닌 if문, for문, while문 등의 **코드 블럭 내부에서 선언된 변수는 전역번수**로 간주함.
- let과 const의 경우 함수 뿐만 아니라 코드블럭 내에서 선언된 변수는 내부에서만 참조 가능
<br/>

## 호이스팅
자바스크립트는 변수 선언문을 미리 실행해두기 때문에 뒤에서 선언된 변수도 앞의 코드에서 참조할 수 있게 된다. 이를 변수 호이스팅이라 함.

|var|let|const|
|-|-|-|
|발생|발생|발생|

- var의 경우 1) 변수 선언 2) undefined로 초기화
- let과 const의 경우 1) 변수 선언 2) 변수 선언문을 만났을 때 초기화

<br/>

## 전역객체 프로퍼티
|var|let|const|
|-|-|-|
|O|X|X|

```JavaScript
// var
var a = 10;
console.log(window.a);	// 10
console.log(a);			// 10
		
// let
let b = 20;
console.log(window.b);	// undefined
console.log(b);			// 20

// const
const c = 30;
console.log(window.c);	// undefined
console.log(c);			// 30
```
- var의 경우 전역객체인 window의 프로퍼티로 할당됨.
- let과 const의 경우 전역객체인 window의 프로퍼티로 할당되지 않음.


<br/><br/>

✨**기본적으로 const를 사용하고, 재할당이 필요한 경우에는 let을 사용하는 것이 좋음**
 

이유

1. var은 중복 선언이 가능하기 때문에  **의도하지 않게 변수 값이 변경**될 수 있음.

2. var은 선언되지 않은 변수에 대해 참조가 가능 (undefined로 초기화 시켜놓음)

3. 함수 외의 모든 코드 블록에서 선언한 변수는 전역변수로 사용 가능

```JavaScript
// var
var myList = [];

for(var i = 0; i < 5; i++) {
	myList.push(function(){
		console.log(i);
	})
}

myList[0]();	// 5
myList[3]();	// 5
 
 
// let
var myList = [];

for(let i = 0; i < 5; i++) {
	myList.push(function(){
		console.log(i);
	})
}

myList[0]();	// 0
myList[3]();	// 3
```

<br/>

#### [참고]
[1](https://curryyou.tistory.com/192)
