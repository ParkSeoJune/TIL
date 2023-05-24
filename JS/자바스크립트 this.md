# 자바스크립트 this

### this 정의

```javascript
let group = {
  title: "1모둠",
  students: ["보라", "호진", "지민"],

  title2: this.title,
  title3() {
    console.log(this.title);
  },
};

console.log(group.title2); //undefined
group.title3(); // 1모둠
```

> this는 함수의 블록 스코프 내에서 선언 되어야 작동한다

브라우저 콘솔(F12)를 키고, this를 쳐보면

```javascript
this; // Window {}
```

변수와 함수 안에 넣어서 해보면

```javascript
var ga = "Global variable";
console.log(this.ga); // === window.ga

function a() {
  console.log(this);
}
a(); // Window {}
```

window이다.  
(함수일 경우 strict 모드일 경우는 undefined)

여기서 한 가지 사실을 알 수 있는데  
this는 기본적으로 **window**라는 것이다

- 일반 함수 내에서 혼자 this를 선언하면, 그 this는 window객체를 가르킨다

일반 함수가 아닌 객체의 메서드의 경우를 보면

```javascript
var obj = {
  a: function () {
    console.log(this);
  },
};
obj.a(); // obj
```

객체 메서드 안의 a 안의 this는 객체 obj를 가리킨다
이것은 객체의 메서드를 호출할 때 this를 내부적으로 바꿔주기 때문이다

단 위의 예제에서 다음과 같이 하면 결과가 달라진다

```javascript
var a2 = obj.a;
a2(); // window
```

a2는 obj.a를 꺼내온 것이기 때문에 더 이상 obj의 메서드가 아니고 변수에 담긴 그냥 일반함수이다

> 호출할 때, 호출하는 함수가 객체의 메서드 인지 그냥 함수인지가 중요하다

---

### 함수 호출 방식과 this 바인딩

자바스크립트의 경우 함수 호출 방식에 의해 this에 바인딩할 어떤 객체가 동적으로 결정된다

다시 말해, 함수를 선언할 때 this에 바인딩할 객체가 정적으로 결정되는 것이 아니고  
함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 this에 바인딩할 객체가 동적으로 결정된다

함수의 호출 방식은 아래와 같이 다양하다

- 함수호출
- 메소드 호출
- 생성자 함수 호출
- 콜백 호출
- apply/call/bind 호출

this는 기본적으로 window이지만,

객체 메서드, bind call apply, new일 때 this가 바뀐다.  
그리고 이벤트리스너나 기타 document라이브러리처럼 this를 내부적으로 바꿀 수도 있으니  
항상 this를 확인해봐야 한다.

선언한 function의 this는 항상 window라는 것 알아두자.  
(strict 모드에서는 undefined !!)

​

this 값은 런타임에 결정된다  
함수를 선언할 때 this를 사용할 수 있다.  
다만, 함수가 호출되기 전까지 this엔 값이 할당되지 않는다.

​

함수를 복사해 객체 간 전달할 수 있다.  
함수를 객체 프로퍼티에 저장해 object.method()같이 ‘메서드’ 형태로 호출하면 this는 object를 참조한다.

​

화살표 함수는 자신만의 this를 가지지 않는다는 점에서 독특하다.  
화살표 함수 안에서 this를 사용하면, 외부에서 this 값을 가져온다.
