---
layout: single
title:  "클린코드 꿀팁"
typora-copy-images-to: ..\images\2021-08-26
---

## 클린코드

### 클린코드란 무엇인가?

좋은 코드는 팀원들이 읽기만해도 무엇인지 이해가 되고

혼자서 일한다고 해도 6개월 뒤에 그 코드를 봤을 때 6개월전에 너가 하던 고민이 무엇인지 알 수 있는 코드




### 팁 첫번째 - 검색 가능한 이름을 써라.

예를 들면 하루가 총 몇초인지 요구하는 함수가 있다면

86400이라는 숫자를 다른사람이 이해 못할 수 있으므로 SECONDS_IN_A_DAY와 같이 사용하자



```javascript
setInterval(eatKimch,86400)
```

86400을 이해 못할 수 있다.

```javascript
const SECONDS_IN_A_DAY = 86400;
setInterval(eatKimchi,SECONDS_IN_A_DAY)
```



### 팁 두번째 - 함수명은 반드시 동사를 써라.



```javascript
function userData(){
    // ...
}

const data = userData();
```

"유저 데이터"는 함수명으로 좋은 이름이 아니다.

```javascript
function loadUserData(){
    // ...
}

const data = loadUserData();
```

"유저 데이터 불러오기"로 바꿔주면 훨씬 이해하기 쉬워진다.



이렇게 이름을 짓다보면 함수가 너무 많은 역할을 수행 하는것이 아닌지 알게 된다.

함수의 이름을 동사로 짓게 된다면 구분의 필요성을 느끼게 되기도 할것이다.



### 팁 세번째 - 몇개의 인수를 함수가 가져야할나

가장 좋은 숫자는 3개 혹은 그 이하라고 생각한다.

만약 너무 많은 인수가 있다면 어떤 인수가 무엇을 하는지 혼란스러울 수 있다.

대신 함수가 많은 숫자의 인수를 요구한다면 한개의 **configuration object**를 보내는 것을 추천한다.

```javascript
function makePayment({price, productId, size, quantity, userId}){
	// process payment
}

makePayment({
    price: 35,
    productId: 5,
    size: "xl",
    quantity: 2,
    userId: "니꼬",
});
```



### 팁 네번째 - boolean 값을 인수로 함수에 보내는 것을 최대한 방지하도록 하자

```javascript
function sendMessage(text, isPrivate){
    if(isPrivate){
        
    }else{
        
    }
}

sendMessage("hello", false)
sendMessage("this is a secret", true)
```

boolean 값을 함수에 보낸다는 것은. 그 함수 안에 if, else가 있다는 뜻이고,

추천하는것은 각각의 if-else값을 다른 함수로 분리하는것이 좋다.

```javascript
function sendPrivateMessage(text){
    // ...
}
function sendPublicMessage(text){
    // ...
}

sendPublicMessage("hello")
sendPrivateMessage("this is a secret")

```



### 팁 다섯번째 - 짧은 변수명이나 축약어 사용을 피하자

```javascript
allUsers.forEach((u,i) => {
	sendEmail(u);
	addToCount(i);
});
```

이렇게 사용하면 아무도 이해할 수 없다.

```javascript
allUsers.forEach((user,currentNumber) => {
	sendEmail(user);
	addToCount(currentNumber);
});
```

