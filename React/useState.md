# useState

## state란?

컴포넌트가 가질 수 있는 상태를 말한다.  
예를 들어 시간이라는 컴포넌트가 있으면 state로 현재 시간이라를 가질 수 있다.

## import

```javascript
import { useState } from "react";
```

react Hooks의 useState는 컴포넌트의 state를 간편하게 생성하고 업데이트를 시킬 수 있게 해주는 도구를 제공한다.  
useState를 사용하기 위해서 react에서 import를 받아야 한다.

## 변수 선언

```javascript
const [state, setState] = useState(초기값);
```

위와 같이 state의 생성과 동시에 가져야 할 초기값을 useState함수의 인자로 넣어주면  
state와 setState라는 두 가지 요소를 배열 형태로 리턴해준다.  
이때 state명은 알맞게 설정하고 두 번째 요소에 set을 붙여주면 된다.

## 변수 재선언

```javascript
setState(1); // state 값을 1로 변경
```

setState 함수를 이용해서 state의 값을 변경하면 해당 컴포넌트는 화면에 다시 렌더링 되어  
state가 변경될 때마다 화면이 업데이트 된다.  
예를 들면 state가 시간이라고 가정한다면, 시간이 변경될 때마다 화면이 다시 렌더링되는 것을 의미한다.

## 예시 코드

```javascript
import { useState } from "react";
import "./App.css";

function App() {
  const [time, setTime] = useState(1);

  const onClick = () => {
    setTime(time + 1);
  };

  console.log("time 업데이트 -> ", time);

  return (
    <div className="App">
      <header className="App-header">
        <span>현재시간: {time}시</span>
        <button onClick={onClick}>update</button>
      </header>
    </div>
  );
}

export default App;
```
