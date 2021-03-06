# ๐ก **Redux Tookit(RTK)**

- ๋ถํ์ํ ์ฝ๋๋ฅผ ์ค์ฌ redux๋ฅผ ๋ ํจ์จ์ ์ผ๋ก ์ฌ์ฉํ  ์ ์๊ฒ ํ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ
- immer ๋ผ์ด๋ธ๋ฌ๋ฆฌ๋ฅผ ์ฌ์ฉํด redux์ ๋ถ๋ณ์ฑ์ ์งํฌ ์ ์์
  - ์ํํ ์ฝ๋ฉ์ ์ํด redux tookit์ ์ฌ์ฉํด ์ํ๋ฅผ ๋ณํ์์ผ๋ immer ๋ผ์ด๋ธ๋ฌ๋ฆฌ๊ฐ ์๋์ ์ผ๋ก ์ํ๋ฅผ ๋ณํํ์ง ์๋ ๊ฒ์ผ๋ก ๋ง๋ค์ด์ฃผ๋ฉฐ ๋ถ๋ณ์ฑ์ ์ง์ผ์ค

# ๐ก **Redux Tookit ์ค์น ๋ฐฉ๋ฒ**

```js
$ npm install @reduxjs/toolkit
$ yarn add @reduxjs/toolkit
```

# ๐ก **Redux Tookit ํจ์**

### โ createAction

- ํจ์๋ก ์ ์ํ action ์ฝ๋๋ฅผ ์งง๊ฒ ๋ง๋ค์ด ์ฃผ๋ ํจ์

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

  - type๊ณผ payload ๋ ๊ฐ์ ์ธ์๋ฅผ ๊ฐ์ง

- **type &** **payload**
  - action์ ์ด๋ ํ ๊ฐ์ ๋ณด๋ด๋  payload์ ํจ๊ป ์ ๋ฌ๋จ
  - action์ text ๋๋ id ๊ฐ์ ๋ฐ๋ก ์กด์ฌํ์ง ์๊ณ  ๋ชจ๋ payload๋ก ์ ์๋จ
  - addToDo.type === โADDโ

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

### โ createReduce

- switch & case๋ฌธ์ ์ฌ์ฉํ์ง ์๊ณ  ์ฌ์ฉ ๊ฐ๋ฅ
- createReducer์ ์ฒซ๋ฒ์งธ ์ธ์๋ initialState
- ์ํ๋ฅผ ๋ณ๊ฒฝํ๊ฑฐ๋ ์๋ก์ด ์ํ ๋ฐํ ์ค ์ ํํ  ์ ์์
  - mutate ๊ฐ๋ฅํ ์ด์ ? redux toolkit๊ณผ immer๊ฐ ์๋์ผ๋ก ์ฌ์ฉ ๊ฐ๋ฅํ๊ฒ๋ ๋ง๋ค์ด์ค

```js
// After
const reducer = createReducer([], {
  [addToDo]: (state, action) => {
    // state์ ์๋ก์ด ๊ฐ์ pushํด์ค
    // push() : ๊ธฐ์กด state mutate
    state.push({ text: action.payload, id: Date.now() });
  },
  [deleteToDo]: (state, action) =>
    // filter() : ์๋ก์ด array return
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

### โ configureStore

- Redux development tools ์ฌ์ฉ ๊ฐ๋ฅ

```js
const store = configureStore({ reducer });
```

### โ createSlice

- createSlice๋ฅผ ์ฌ์ฉํ๋ฉด ์ฝ๋ ์์ ๋์ฑ ์ค์ผ ์ ์์
- reducer๋ฟ๋ง ์๋๋ผ actions๋ ์์ฑ
- option์ผ๋ก name, initialState, reducers๋ฅผ ๋ฐ์
- add์ remove๊ฐ toDos์ action

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
