# Call & Bind & Apply 함수 정리

### Call

함수를 호출하는 방법으로는 함수 뒤에 ()를 붙이는 것과 call 그리고 apply하는 방법이 있다.

```javascript
var example = function (a, b, c) {
  return a + b + c;
};
example(1, 2, 3);
example.call(null, 1, 2, 3);
example.apply(null, [1, 2, 3]);
```

call은 보통 함수와 똑같이 인자를 넣고, apply는 인자를 하나로 묶어 배열로 만들어 넣는 것을 알 수 있다.

그렇다면 call과 apply가 공통적으로 가진 **null**의 역할은 뭘까?

바로 **this**를 대체하는 것이다.

```javascript
var obj = {
  string: "zero",
  yell: function () {
    alert(this.string);
  },
};
var obj2 = {
  string: "what",
};

obj.yell(); // 'zero';
obj.yell.call(obj2); // 'what'
// obj1.yell()을 obj2.yell()로 바꾼 효과라고 보면 된다.
```

마지막 줄에서 obj.yell.call(obj2)로 this가 가리키는 것을 obj1에서 obj2로 바꾸었다.

yell은 obj의 메소드인데도 zero 대신에 what이 alert되었다.

```javascript
var kim = { name: "kim", first: 10, second: 20 };
var lee = { name: "lee", first: 100, second: 200 };

function sum(num) {
  return num + this.first + this.second;
}

sum.call(kim, 500); //sum을 call하는데 this값을 kim객체로 한다
```

자바스크립트에서는 함수도 객체이기 때문에, 본래라면 전역window에 this가 걸린 것을 저런식으로도 지정이 가능하다.

**즉 call을 써서 this를 정의해준다면 다른 객체의 파라미터나 메소드를 자기 것마냥 사용할 수 있다.**

this는 기본으로 전역객체의 window로 지정되어 있다.  
하지만 몇 가지 방법으로 window를 다른 것으로 바꿀 수 있다.  
그 방법으로는 `call`, `bind`, `apply`에서 첫 번째 인자로 다른 것을 넣어주는게 this를 바꾸는 방법 중 하나이다.

위의 메소드를 쓰는 예는 **함수의 arguments를 조작할 때** 사용하는 것이다.

> arguments는 함수라면 처음부터 갖고 있는 숨겨진 속성이다.  
> 바로 함수에 들어온 **인자를 배열 형식**으로 반환한다. (배열이 아닌 유사배열이라고 부름)

```javascript
function example() {
  console.log(arguments);
}
example(1, "string", true); // [1, 'string', true]
```

생긴 건 배열이지만, 배열이 아닌 유사배열이기 때문에, 배열의 메소드는 쓸 수 없다.

하지만 call이나 apply를 사용하면 배열의 메소드를 쓸 수 있다.

```javascript
function example() {
  console.log(Array.prototype.join.call(arguments));
}

example(1, "string", true);
```

배열의 프로토타입에 있는 join 함수를 빌려 쓰는 것이다. this는 arguments를 가리키게 한다.

1.  join()으로 배열을 문자열로 변환하려고 한다.
2.  함수 인자들로 값을 넘긴다. arguments로 배열형태로 받겠지만, 유사배열이라 arguments.join()같은 것은 안됨.
3.  그래서 우선은 프로토타입 메서드 Array.prototype.join()을 불러오고 그 뒤에 **.call()로 join함수를 조작**한다.
4.  call(arguments)로 this를 유사배열로 가리키게 한다. 본래는 Array객체를 가리키고 있지만 바꾼 것이다.  
    그러면 Array.prototype.join()이 최종적으로 [1, 'string', true].join()이 된다.

---

### apply

apply() 메소드의 대표적인 용도는 arguments 객체와 같은, 유사 배열 객체에 배열 메소드를 사용하는 경우이다.

arguments 객체는 배열이 아니기 때문에 Array객체의 slice() 같은 배열의 메소드를 사용할 수 없지만  
 apply() 메소드를 이용하면 가능하다.

```javascript
function convertArgsToArray() {
  console.log(arguments);

  // arguments 유사 배열 객체를 사용
  // slice: 배열의 특정 부분에 대한 복사본을 생성
  var arr = Array.prototype.slice.apply(arguments); // arguments.slice
  // var arr = [].slice.apply(arguments);

  console.log(arr);
  return arr;
}

convertArgsToArray(1, 2, 3); //[1,2,3]
```

Array.prototype.slice.apply(arguments)는,

> "Array.prototype.slice() 메소드를 호출한다. 단 this는 arguments 객체로 바인딩해라"는 의미가 된다.

결국 Array.prototype.slice() 메소드를 arguments 객체 자신의 메소드인 것처럼 arguments.slice()와 같은 형태로 호춣하라는 의미이다.

---

### bind

bind 함수는 함수가 가리키는 this만 바꾸고 호출하지 않는 것이다.  
정확히 말하면 this를 정의하고 나서 그 함수를 복사해 새로운 함수를 만들어 리턴하는 것이다.

```javascript
var obj = {
  string: "zero",
  yell: function () {
    alert(this.string);
  },
};
var obj2 = {
  string: "what",
};

var yell2 = obj.yell.bind(obj2);
yell2(); // 'what'
obj.yell.bind(obj2)(); // 'what'
```

obj.yell.bind(obj2)했더니 yell 함수의 this가 obj2로 바뀌었다.

**즉 call이나 apply와 비슷하지만 호출은 하지 않고 함수만 변환하는 것이다.**
