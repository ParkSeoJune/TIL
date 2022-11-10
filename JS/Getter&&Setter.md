## Getter함수와 Setter 함수   
***
   
객체 안에 Getter 함수를 설정하는 방법   
객체를 만들면, 다음과 같이 객체안의 값을 수정할 수도 있다.   
   
```
const numbers = {
  a: 1,
  b: 2
};

numbers.a = 5;
cosole.log(numbers);
```
   
또한 특정 값을 바꾸거나 조회하려고 할 때 원하는 코드를 실행 시킬 수 있다.   
   
```
const number = {
  a: 1,
  b:2,
  get sum() {
    console.log('sum 함수가 실행됩니다!');
    return this.a + this.b;
  }
};

console.log(numbers.sum);
numbers.b = 5;
console.log(numbers.sum);
```
   
결과를 보면 number.sum을 조회했을 뿐인데 함수가 실행되고 그 결과값이 출력되는걸 알 수 있다.   
   
Setter 함수를 사용해보면   
   
```
const numbers = {
  _a: 1,
  _b: 2,
  sum: 3,
  calculate() {
    console.log('calculate');
    this.sum = this._a + this._b;
  },
  get a() {
    return this._a;
  },
  get b() {
    return this._b;
  },
  set a(value) {
    console.log('a가 바뀝니다.');
    this._a = value;
    this.calculate();
  },
  set b(value) {
    console.log('b가 바뀝니다.');
    this._b = value;
    this.calculate();
  }
};

console.log(numbers.sum);
numbers.a = 5;
numbers.b = 7;
numbers.a = 9;
console.log(numbers.sum);
console.log(numbers.sum);
console.log(numbers.sum);
```
   
Setter 함수를 설정할 때에는 함수의 앞부분에 set 키워드를 붙인다.   
   
Getter 함수를 써볼 때에는 numbers.sum이 조회가 될 때마다 덧셈이 이루었지만,   
이제는 a 혹은 b 값이 바뀔 때마다 sum 값을 연산한다.