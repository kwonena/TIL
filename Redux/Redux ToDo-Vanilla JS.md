# 💡 **To Do 상세 코드**

### ✔ **추가, 삭제 action 등록**

```js
const ADD_TODO = "ADD_TODO";
const DELETE_TODO = "DELETE_TODO";

// action만 return 해주는 함수
// 함수를 작은 단위로 쪼개 최적화 할 수 있음
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

### ✔ **reducer 등록**

- state를 mutation(변형)하면 안 되기 때문에 조건에 맞는 요소들로 새로운 배열을 만들어주는 **filter 함수**를 선택

```js
// store을 수정할 수 있는 방법은 action을 보내는 것뿐
// state는 single source of truth, read-only
// state는 mutation(변형) 금지 -> new state objects를 리턴
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

### ✔ **dispatch**

- dispatch만 하는 함수를 생성해 action이 등록된 함수에 파라미터 전달 후 호출

```js
const dispatchAddToDo = (text) => {
  store.dispatch(addToDo(text));
};

const dispatchDeleteToDo = (e) => {
  // 삭제 버튼을 누른 부모 노드를 찾아 삭제
  const id = parseInt(e.target.parenNode.id);
  store.dispatch(deleteToDo(id));
};
```

### ✔ **To Do List 화면 등록 함수**

- state에 새로운 변화가 생기면 호출되는 함수
- ul에 새로운 To Do li를 추가해 웹 페이지에 실질적으로 나타나는 함수
- ul.innerHTML을 “” 빈 요소로 만들어 그 전의 값이 다시 저장되는 오류가 발생하지 않도록 함
- forEach문을 사용해 모든 toDo 요소를 화면에 그림
- 삭제 버튼을 누르면 삭제 이벤트가 발생해야함으로 버튼에도 addEventListener를 등록하고 dispatchDeleteToDo를 호출함

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

### ✔ **To Do List 요소 등록 함수**

```js
const onSubmit = (e) => {
  e.preventDefault();
  const toDo = input.value;
  input.value = "";
  dispatchAddToDo(toDo);
};

form.addEventListener("submit", onSubmit);
```

# 💡 **전체 코드**

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

// action만 return 해주는 함수
// 함수를 작은 단위로 쪼개 최적화 할 수 있음
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

// store을 수정할 수 있는 방법은 action을 보내는 것뿐
// state는 single source of truth, read-only
// state는 mutation(변형) 금지 -> new state objects를 리턴
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
  // 삭제 버튼을 누른 부모 노드를 찾아 삭제
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

📌 **createStore에 가로 선이 생기는 경우**

```js
$ npm remove redux react-redux
$ npm install redux@4.1.2 react-redux
```
