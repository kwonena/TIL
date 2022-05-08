# 💡 **Redux Tookit(RTK)**

- 불필요한 코드를 줄여 redux를 더 효율적으로 사용할 수 있게 하는 라이브러리
- immer 라이브러리를 사용해 redux의 불변성을 지킬 수 있음
  - 원활한 코딩을 위해 redux tookit을 사용해 상태를 변환시켜도 immer 라이브러리가 자동적으로 상태를 변환하지 않는 것으로 만들어주며 불변성을 지켜줌

# 💡 **Redux Tookit 설치 방법**

```js
$ npm install @reduxjs/toolkit
$ yarn add @reduxjs/toolkit
```

# 💡 **Redux Tookit 함수**

### ✔ createAction

- 함수로 정의한 action 코드를 짧게 만들어 주는 함수

```js
// After
const addToDo = createAction("ADD");
```

```js
// Before
const ADD_TODO = "ADD_TODO";

const addToDo = (text) => {
  return {
    type: ADD_TODO,
    text,
  };
};
```

- **addToDo()**

  - type과 payload 두 개의 인자를 가짐

- **type &** **payload**
  - action에 어떠한 값을 보내든 payload와 함께 전달됨
  - action에 text 또는 id 값은 따로 존재하지 않고 모두 payload로 정의됨
  - addToDo.type === “ADD”

```js
// After
const reducer = (state = [], action) => {
  switch (action.type) {
    case **addToDo.type**:
			return [...state, { text: action.**payload**, id: Date.now() }];
    case **deleteToDo.type**:
      return state.filter((toDo) => toDo.id !== action.**payload**);
    default:
      return state;
  }
};
```

```js
// Before
const reducer = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      return [...state, { text: action.text, id: Date.now() }];
    case DELETE_TODO:
      return state.filter((toDo) => toDo.id !== action.id);
    default:
      return state;
  }
};
```

### ✔ createReduce

- switch & case문을 사용하지 않고 사용 가능
- createReducer의 첫번째 인자는 initialState
- 상태를 변경하거나 새로운 상태 반환 중 선택할 수 있음
  - mutate 가능한 이유? redux toolkit과 immer가 자동으로 사용 가능하게끔 만들어줌

```js
// After
const reducer = createReducer([], {
  [addToDo]: (state, action) => {
    // state에 새로운 값을 push해줌
    // push() : 기존 state mutate
    state.push({ text: action.payload, id: Date.now() });
  },
  [deleteToDo]: (state, action) =>
    // filter() : 새로운 array return
    state.filter((toDo) => toDo.id !== action.payload),
});
```

```js
// Before
const reducer = (state = [], action) => {
  switch (action.type) {
    case addToDo.type:
      return [...state, { text: action.payload, id: Date.now() }];
    case deleteToDo.type:
      return state.filter((toDo) => toDo.id !== action.payload);
    default:
      return state;
  }
};
```

### ✔ configureStore

- Redux development tools 사용 가능

```js
const store = configureStore({ reducer });
```

### ✔ createSlice

- createSlice를 사용하면 코드 양을 더욱 줄일 수 있음
- reducer뿐만 아니라 actions도 생성
- option으로 name, initialState, reducers를 받음
- add와 remove가 toDos의 action

```js
import { configureStore, createSlice } from "@reduxjs/toolkit";

const toDos = createSlice({
  name: "toDosReducer",
  initialState: [],
  reducers: {
    add: (state, action) => {
      state.push({ text: action.payload, id: Date.now() });
    },
    remove: (state, action) =>
      state.filter((toDo) => toDo.id !== action.payload),
  },
});

const store = configureStore({ reducer: toDos.reducer });

export const { add, remove } = toDos.actions;

export default store;
```
