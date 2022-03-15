# 💡 React Hook

---

함수형 컴포넌트에서도 클래스형 컴포넌트의 기능을 쓸 수 있게끔 만들어진 기술이다. 기존 함수형 컴포넌트에서는 사용할 수 없었던 상태 관리, Lifecylce 메소드등을 사용할 수 있다.

# 💡 사용 방법

---

기본적으로 React Hook은 useState함수를 통해 state를 호출하여 상태 관리를 한다. 사용할 변수와 그 변수의 상태 관리를 해줄 함수를 호출하고 useState함수에서 기본값을 설정해 사용힌다.

num과 setNum 두개를 선언한 후 useState를 호출하게 되면 리액트에서 실제 state값인 num과 num을 업데이트 해줄 수 있는 함수 setNum 두가지를 return 해준다.

```
import React, { useState } from 'react'; //useState 함수 사용 선언

function Counter() {
    const [num, setNum] = useState(0);
		//사용할 num의 기본값은 0, num을 바꿔주는 setNum 함수

    const increase = () => {
        setNum(num + 1);
    };

    return (
     <div>
         <h1>{num}</h1>
         <button onClick={increase}>+1</button>
     </div>
    );
  }

  export default Counter;
```

마찬가지로 함수형 컴포넌트이기 때문에 코드 안에 있는 props나 state, 지역변수들이 계속 **반복적으로 호출**된다.

### ❓ 계속 호출되면 useState가 0으로 초기화 되지 않을까?

useState는 리액트 훅에서 제공하는 API 중에 하나로 useState를 사용하면 리액트가 자동으로 기억하고 있다. 그래서 초기화 되지 않고 동일한 값을 받아올 수 있다.

# 💡 Ref를 사용할 때

---

기존 **클래스형 컴포넌트**에서 Ref를 사용할 땐 createRef() 함수를 이용했다.

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

하지만 state가 변경될 때마다 코드블럭이 계속해서 실행되는 **함수형 컴포넌트**에서는 Ref를 반복적으로 만들지 않기 위해서 리액트 훅에서 제공하는 **useRef()** 함수를 사용한다. 매번 새로운 레퍼런스를 만들지 않고 한 번 만든 것을 재사용할 수 있게 해준다.

```
import React, { useRef, useState } from "react";

const Test = props => {
	const spanRef = useRef();

	return (
		<span ref={spanRef}></span>
	);
};

export default Test;
```

# 💡 Lifecylce 함수 사용하기

---

리액트 훅을 사용하면 함수형 컴포넌트에서도 **Lifecylce 함수**를 사용할 수 있다.

클래스형 컴포넌트에서는 componentDidMount()와 componentDidUpdate() 두가지가 필요할 때 코드를 중복해서 두가지를 모두 호출하는 경우가 있다.

```
import React, { Component } from "react";

class Test extends Component {
	componentDidMount() {
		console.log('mounted!');
	}
	componentDidUpdate() {
		console.log('updated!');
	}

render() {}

export default Test;
```

리액트 훅에서는 클래스형 컴포넌트에 이러한 점을 보완하여 componentDidMount()와 componentDidUpdate() 두 개의 함수를 \*\*useEffect()\*\*라는 함수를 통해 한 번만 정의해서 사용할 수 있게 해준다.

```
import React, { useRef, useState } from "react";

const Test = props => {
	useEffect(() => {
    console.log('mounted & updated!');
  });

	return ();
};

export default Test;
```

컴포넌트가 업데이트 될 때마다 함수를 불러오는 것이 아닌 어떤 값이 변경되어 **필요할 때만 호출**할 수 있도록 만드는 것이 더 유용하다.

```
useEffect(() => {
    console.log('mounted & updated!');
}, [count]);
```

useEffect()에 변수를 전달하면 변수가 변경될 때만 호출하게 할 수 있다.
