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
yell은 obj의 메소드인데도 zero 대신에 what이 alert되었습니다.

```javascript
var kim = { name: "kim", first: 10, second: 20 };
var lee = { name: "lee", first: 100, second: 200 };

function sum(num) {
  return num + this.first + this.second;
}

sum.call(kim, 500); //sum을 call하는데 this값을 kim객체로 한다
```

자바스크립트에서는 함수도 객체이기 때문에, 본래라면 전역window에 this가 걸린 것을 저런식으로도 지정이 가능합니다.

**즉 call을 써서 this를 정의해준다면 다른 객체의 파라미터나 메소드를 자기 것마냥 사용할 수 있습니다.**

this는 기본으로 전역객체의 window로 지정되어 있습니다.  
하지만 몇 가지 방법으로 window를 다른 것으로 바꿀 수 있습니다.  
그 방법으로는 `call`, `bind`, `apply`에서 첫 번째 인자로 다른 것을 넣어주는게 this를 바꾸는 방법 중 하나입니다.
