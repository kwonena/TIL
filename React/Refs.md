# 💡 Refs

---

리액트에서 특정 요소에 접근하여 **레퍼런스 값을 받아올 수 있게 해주는 것**이다.

리액트에서는 DOM 요소를 직접적으로 사용하지 않기 때문에 다른 리액트 요소에 접근하고 싶다면 Refs를 활용한다.

# 💡 Ref 사용

---

- 접근하고자 하는 요소의 멤버 변수를 createRef() 함수를 호출해 만든다.
- 레퍼런스 값을 원하는 요소의 Ref에 전달해준다.
- input에 inputRef를 연결해주면 해당하는 데이터를 읽어올 수 있게 된다.

```
import React, { Component } from "react";

class Test extends Component {
  inputRef = React.createRef();

  render() {
    return <input ref={this.inputRef} className="testInput" />;
  }
}

export default Test;
```

**➕ createRef()는 클래스형 컴포넌트, useRef()는 함수형 컴포넌트에서 사용한다.**

# 💡 useRef를 이용한 변수

---

useRef 함수를 이용해 변수를 저장하면 변수의 값이 변경될 때 불필요한 re-rendering은 되지 않고, 컴포넌트에 변수의 값은 저장할 수 있다.

useState를 이용하면 state의 값이 변경될때마다 re-rendering 되는데 굳이 re-rendering이 필요없는 **간단한 데이터를 관리할 때 사용**하면 유용하다.

```
const nextId = useRef(4);
```
