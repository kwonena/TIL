# ๐ก **To Do ์์ธ ์ฝ๋**

### โ **์ถ๊ฐ, ์ญ์  action ๋ฑ๋ก**

```js
const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

// action๋ง return ํด์ฃผ๋ ํจ์
// ํจ์๋ฅผ ์์ ๋จ์๋ก ์ชผ๊ฐ ์ต์ ํ ํ  ์ ์์
const addToDo = (text) => {
  return {
    type: ADD_TODO,
    text,
  };
};

const deleteToDo = (id) => {
  return {
    type: DELETE_TODO,
    id,
  };
};
```

### โ **reducer ๋ฑ๋ก**

- state๋ฅผ mutation(๋ณํ)ํ๋ฉด ์ ๋๊ธฐ ๋๋ฌธ์ ์กฐ๊ฑด์ ๋ง๋ ์์๋ค๋ก ์๋ก์ด ๋ฐฐ์ด์ ๋ง๋ค์ด์ฃผ๋ **filter ํจ์**๋ฅผ ์ ํ

```js
// store์ ์์ ํ  ์ ์๋ ๋ฐฉ๋ฒ์ action์ ๋ณด๋ด๋ ๊ฒ๋ฟ
// state๋ single source of truth, read-only
// state๋ mutation(๋ณํ) ๊ธ์ง -> new state objects๋ฅผ ๋ฆฌํด
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

### โ **dispatch**

- dispatch๋ง ํ๋ ํจ์๋ฅผ ์์ฑํด action์ด ๋ฑ๋ก๋ ํจ์์ ํ๋ผ๋ฏธํฐ ์ ๋ฌ ํ ํธ์ถ

```js
const dispatchAddToDo = (text) => {
  store.dispatch(addToDo(text));
};

const dispatchDeleteToDo = (e) => {
  // ์ญ์  ๋ฒํผ์ ๋๋ฅธ ๋ถ๋ชจ ๋ธ๋๋ฅผ ์ฐพ์ ์ญ์ 
  const id = parseInt(e.target.parenNode.id);
  store.dispatch(deleteToDo(id));
};
```

### โ **To Do List ํ๋ฉด ๋ฑ๋ก ํจ์**

- state์ ์๋ก์ด ๋ณํ๊ฐ ์๊ธฐ๋ฉด ํธ์ถ๋๋ ํจ์
- ul์ ์๋ก์ด To Do li๋ฅผ ์ถ๊ฐํด ์น ํ์ด์ง์ ์ค์ง์ ์ผ๋ก ๋ํ๋๋ ํจ์
- ul.innerHTML์ โโ ๋น ์์๋ก ๋ง๋ค์ด ๊ทธ ์ ์ ๊ฐ์ด ๋ค์ ์ ์ฅ๋๋ ์ค๋ฅ๊ฐ ๋ฐ์ํ์ง ์๋๋ก ํจ
- forEach๋ฌธ์ ์ฌ์ฉํด ๋ชจ๋  toDo ์์๋ฅผ ํ๋ฉด์ ๊ทธ๋ฆผ
- ์ญ์  ๋ฒํผ์ ๋๋ฅด๋ฉด ์ญ์  ์ด๋ฒคํธ๊ฐ ๋ฐ์ํด์ผํจ์ผ๋ก ๋ฒํผ์๋ addEventListener๋ฅผ ๋ฑ๋กํ๊ณ  dispatchDeleteToDo๋ฅผ ํธ์ถํจ

```js
const paintToDos = () => {
  const toDos = store.getState();
  ul.innerHTML = "";
  toDos.forEach((toDo) => {
    const li = document.createElement("li");
    const btn = document.createElement("button");
    btn.innerText = "DEL";
    btn.addEventListener("click", dispatchDeleteToDo);
    li.id = toDo.id;
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  });
};

store.subscribe(paintToDos);
```

### โ **To Do List ์์ ๋ฑ๋ก ํจ์**

```js
const onSubmit = (e) => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  dispatchAddToDo(toDo);
};

form.addEventListener("submit", onSubmit);
```

# ๐ก **์ ์ฒด ์ฝ๋**

```html
<body>
  <h1>To Dos</h1>
  <form>
    <input type="text" placeholder="Write to do" />
    <button>Add</button>
  </form>
  <ul></ul>
</body>
```

```js
import { createStore } from "redux";

const form = document.querySelector("form");
const input = document.querySelector("input");
const ul = document.querySelector("ul");

const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

// action๋ง return ํด์ฃผ๋ ํจ์
// ํจ์๋ฅผ ์์ ๋จ์๋ก ์ชผ๊ฐ ์ต์ ํ ํ  ์ ์์
const addToDo = (text) => {
  return {
    type: ADD_TODO,
    text,
  };
};

const deleteToDo = (id) => {
  return {
    type: DELETE_TODO,
    id,
  };
};

// store์ ์์ ํ  ์ ์๋ ๋ฐฉ๋ฒ์ action์ ๋ณด๋ด๋ ๊ฒ๋ฟ
// state๋ single source of truth, read-only
// state๋ mutation(๋ณํ) ๊ธ์ง -> new state objects๋ฅผ ๋ฆฌํด
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

const store = createStore(reducer);

store.subscribe(() => console.log(store.getState()));

const dispatchAddToDo = (text) => {
  store.dispatch(addToDo(text));
};

const dispatchDeleteToDo = (e) => {
  // ์ญ์  ๋ฒํผ์ ๋๋ฅธ ๋ถ๋ชจ ๋ธ๋๋ฅผ ์ฐพ์ ์ญ์ 
  const id = parseInt(e.target.parenNode.id);
  store.dispatch(deleteToDo(id));
};

const paintToDos = () => {
  const toDos = store.getState();
  ul.innerHTML = "";
  toDos.forEach((toDo) => {
    const li = document.createElement("li");
    const btn = document.createElement("button");
    btn.innerText = "DEL";
    btn.addEventListener("click", dispatchDeleteToDo);
    li.id = toDo.id;
    li.innerText = toDo.text;
    li.appendChild(btn);
    ul.appendChild(li);
  });
};

store.subscribe(paintToDos);

const onSubmit = (e) => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  dispatchAddToDo(toDo);
};

form.addEventListener("submit", onSubmit);
```

๐ **createStore์ ๊ฐ๋ก ์ ์ด ์๊ธฐ๋ ๊ฒฝ์ฐ**

```js
$ npm remove redux react-redux
$ npm install redux@4.1.2 react-redux
```
