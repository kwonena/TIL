# 💡 Component란?

---

재사용이 가능하게끔 만든 **독립적인 UI 조각**이고 리액트에서 사용하는 최소한의 단위이다.

# 💡 Component의 종류

---

### Class component

- Component
- Purecomponent

### Function component

- Function
- memo (Higher Order Component)
- React Hook

# 💡 Component의 기본 구조

---

### ✔ Class Component

- 리액트에서 제공하는 component class를 상속해서 만든다.
- component에 state(object)가 **필요**하며 주기적으로 업데이트 될 때 사용한다.
- state가 변경될 때 component는 render 함수를 호출하며 사용자에게 업데이트 된 내용을 보여준다.
- Life cycle 메소드를 사용할 수 있다.
- 멤버변수에 접근할 때 항상 this를 붙여 접근해야 한다.

```
import React, { Component } from 'react';

class Test extends Component {
  showTestMessage = () => {
    console.log("Hello:)");
  }
  render() {
    return <button onClick={this.showTestMessage}>Click✔</button>
  }
}

export default Test;
```

클래스형 컴포넌트의 기본 구조

### ✔ Function Component

- 간단하게 함수로 만들 수 있는 component이다
- state나 Life cycle 메소드가 **필요없고** 정적으로 데이터가 표기 될 때 사용한다.
- React Hook을 사용하면 Function Component에서도 state나 Life cycle 메소드를 사용할 수 있다.
- const로 지역변수를 할당하며 this를 사용하지 않아도 된다.

```
import React from 'react';

function Test(props) {
  const showTestMessage = () => {
    console.log("Hello:)");
  }
  return <button onClick={showTestMessage}>Click✔</button>
};

export default Test;
```

함수형 컴포넌트의 기본 구조
