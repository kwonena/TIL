# 💡 **Redux**

JavaScript의 상태 관리 라이브러리이다. React뿐만 아니라 Vanilla JS 환경에서도 상태관리를 효율적으로 도와준다.

프로그램 개발을 하는 데에 있어 일관성을 유지하게 하고, 서로 다른 환경에서 작동할 수 있게 하는 장점이 있다.

# 💡 **Redux 설치 방법**

```
$ npm install redux
$ yarn add redux
```

# 💡 **Redux 규칙**

- 하나의 애플리케이션에는 하나의 스토어만 존재
- 상태는 읽기 전용으로 기존의 상태를 건드리지 않음
- Reducer 함수는 똑같은 인자값을 받으면 항상 똑같은 결과값을 반환해야 함

# 💡 **Redux의 구성 요소**

### ✔ Store (스토어)

```
// store : date 저장 공간
const countStore = createStore(countModifier);
```

### ✔ Action (액션)

```
// action : reducer와 소통하는 방식
// action type을 변수화 시켜 오류를 쉽게 잡을 수 있게 만듦
// 일반 string 타입은 JS가 오류를 잡지 못함
const ADD = "ADD";
const MINUS = "MINUS";
```

### ✔ Reducer (리듀서)

```
// reducer : data 수정 함수
// 데이터를 유일하게 수정할 수 있는 곳
// 인자로 state 값과 action을 받음
// return 값은 application의 state가 됨
// 주로 switch문을 사용해 action type별로 알맞는 역할을 수행
const countModifier = (count = 0, action) => {
  switch (action.type) {
    case ADD:
      return count + 1;
    case MINUS:
      return count - 1;
    default:
      return count;
  }
};
```

# 💡 **Reducer의 함수들**

### ✔ getState()

```
// 현재 store의 상태를 출력함
console.log(countStore.getState();)
```

### ✔ dispatch()

```
// dispatch : reducer에 action을 보내고 호출함
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};

const handleMinus = () => {
  countStore.dispatch({ type: MINUS });
};
```

### ✔ subscribe()

```
// subscribe : store의 변화를 감지하면 인자 값으로 준 함수를 실행
countStore.subscribe(onChange);
```

# 💡 **전체 코드**

```
<!-- 두 가지의 증감소 버튼을 통해 span의 값을 변경하는 프로그램 -->
<body>
  <button id="add">Add</button>
  <span></span>
  <button id="minus">Minus</button>
</body>
```

```
// createStore : store 생성 함수
import { createStore } from "redux";

const add = document.getElementById("add");
const minus = document.getElementById("minus");
const number = document.querySelector("span");

number.innerText = 0;

// action : reducer와 소통하는 방식
// action type을 변수화 시켜 오류를 쉽게 잡을 수 있게 만듦
// 일반 string 타입은 JS가 오류를 잡지 못함
const ADD = "ADD";
const MINUS = "MINUS";

// reducer : data 수정 함수
// 데이터를 유일하게 수정할 수 있는 곳
// return 값은 application의 data가 됨
const countModifier = (count = 0, action) => {
  switch (action.type) {
    case ADD:
      return count + 1;
    case MINUS:
      return count - 1;
    default:
      return count;
  }
};

// store : date 저장 공간
const countStore = createStore(countModifier);

// store의 현재 상태를 number에 저장함
const onChange = () => {
  number.innerText = countStore.getState();
};

// subscribe : store의 변화를 감지하면 인자 값으로 준 함수를 실행
countStore.subscribe(onChange);

// dispatch : reducer에 action을 보내고 호출함
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};

const handleMinus = () => {
  countStore.dispatch({ type: MINUS });
};

add.addEventListener("click", handleAdd);
minus.addEventListener("click", handleMinus);
```
