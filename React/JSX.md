## JSX의 기본 규칙   
   
***
   
태그는 꼭 닫혀있어야한다.   
HTML에서 <br>같은 태그는 사용할 때 닫지 않고도 사용이 가능했는데   
리액트에서는 그렇게 하면 안된다.   
   
두 개 이상의 태그는 무조건 하나의 태그로 감싸져야 한다.   
```
<div>
  <div>
    <Hello />
    <div>안녕하세요</div>
  </div>
</div>
```
   
이런 방법으로 <div></div>태그를 이용하여 감쌀 수도 있지만   
리액트의 Fragment(<> </>)라는 것을 사용하면 된다.   
   
JSX 안에 자바스크립트 변수를 보여줘야 할 때에는 {} 으로 감싸서 보여준다.   
ex) <div>{name}</div>   
   
style과 className   
JSX에서 태그에 style과 CSS class를 설정하는 방법은 HTML에서 설정하는 방법과 다르다.   
   
우선, 인라인 스타일은 객체 형태로 작성을 해야 하고, background-color처럼 -로 구분되어 있는   
이름들은 backgroundColor처럼 camelCase형태로 네이밍 해준다.   
   
그리고 CSS class를 설정할 때에는 class= 방식이 아닌 className=으로 해줘야 한다.   
   
주석   
JSX 내부의 주석은 {/*주석*/} 으로 작성한다.   