# 💡 React

---

사용자에게 UI를 보여주고 이벤트를 처리할 수 있는 Javascript **라이브러리**이다. 리액트는 **컴포넌트**로 이루어져 재사용이 가능한 웹 어플리케이션을 만들 수 있다.

리액트의 컴포넌트 중 클래스 컴포넌트이다.

```
import React, { Component } from 'react';

class Test extends Component {
  state = {
		count : 0,
	};
  render() {
    return <button onClick={this.count++}>Click✔</button>
  }
}

export default Test;
```

크게 두가지로 state부분과 render 부분으로 나눌 수 있다.

**state**는 컴포넌트에 들어있는 데이터를 나타내는 오브젝트이고,

```
  state = {
		count : 0,
	};
```

**render**는 사용자에게 어떻게 표기될건지 나타내주는 곳이다.

```
   render() {
    return <button onClick={this.count++}>Click✔</button>
  }
```

리액트는 state가 변경이 되면 render 함수가 자동적으로 다시 호출되어 사용자에게 보여지게 된다.
