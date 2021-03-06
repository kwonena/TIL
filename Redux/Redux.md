# ๐ก **Redux**

JavaScript์ ์ํ ๊ด๋ฆฌ ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ด๋ค. React๋ฟ๋ง ์๋๋ผ Vanilla JS ํ๊ฒฝ์์๋ ์ํ๊ด๋ฆฌ๋ฅผ ํจ์จ์ ์ผ๋ก ๋์์ค๋ค.

ํ๋ก๊ทธ๋จ ๊ฐ๋ฐ์ ํ๋ ๋ฐ์ ์์ด ์ผ๊ด์ฑ์ ์ ์งํ๊ฒ ํ๊ณ , ์๋ก ๋ค๋ฅธ ํ๊ฒฝ์์ ์๋ํ  ์ ์๊ฒ ํ๋ ์ฅ์ ์ด ์๋ค.

# ๐ก **Redux ์ค์น ๋ฐฉ๋ฒ**

```js
$ npm install redux
$ yarn add redux
```

# ๐ก **Redux ๊ท์น**

- ํ๋์ ์ ํ๋ฆฌ์ผ์ด์์๋ ํ๋์ ์คํ ์ด๋ง ์กด์ฌ
- ์ํ๋ ์ฝ๊ธฐ ์ ์ฉ์ผ๋ก ๊ธฐ์กด์ ์ํ๋ฅผ ๊ฑด๋๋ฆฌ์ง ์์
- Reducer ํจ์๋ ๋๊ฐ์ ์ธ์๊ฐ์ ๋ฐ์ผ๋ฉด ํญ์ ๋๊ฐ์ ๊ฒฐ๊ณผ๊ฐ์ ๋ฐํํด์ผ ํจ

# ๐ก **Redux์ ๊ตฌ์ฑ ์์**

### โ Store (์คํ ์ด)

```js
// store : date ์ ์ฅ ๊ณต๊ฐ
const countStore = createStore(countModifier);
```

### โ Action (์ก์)

```js
// action : reducer์ ์ํตํ๋ ๋ฐฉ์
// action type์ ๋ณ์ํ ์์ผ ์ค๋ฅ๋ฅผ ์ฝ๊ฒ ์ก์ ์ ์๊ฒ ๋ง๋ฆ
// ์ผ๋ฐ string ํ์์ JS๊ฐ ์ค๋ฅ๋ฅผ ์ก์ง ๋ชปํจ
const ADD = "ADD";
const MINUS = "MINUS";
```

### โ Reducer (๋ฆฌ๋์)

```js
// reducer : data ์์  ํจ์
// ๋ฐ์ดํฐ๋ฅผ ์ ์ผํ๊ฒ ์์ ํ  ์ ์๋ ๊ณณ
// ์ธ์๋ก state ๊ฐ๊ณผ action์ ๋ฐ์
// return ๊ฐ์ application์ state๊ฐ ๋จ
// ์ฃผ๋ก switch๋ฌธ์ ์ฌ์ฉํด action type๋ณ๋ก ์๋ง๋ ์ญํ ์ ์ํ
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

# ๐ก **Reducer์ ํจ์๋ค**

### โ getState()

```js
// ํ์ฌ store์ ์ํ๋ฅผ ์ถ๋ ฅํจ
console.log(countStore.getState();)
```

### โ dispatch()

```js
// dispatch : reducer์ action์ ๋ณด๋ด๊ณ  ํธ์ถํจ
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};

const handleMinus = () => {
  countStore.dispatch({ type: MINUS });
};
```

### โ subscribe()

```js
// subscribe : store์ ๋ณํ๋ฅผ ๊ฐ์งํ๋ฉด ์ธ์ ๊ฐ์ผ๋ก ์ค ํจ์๋ฅผ ์คํ
countStore.subscribe(onChange);
```

# ๐ก **์ ์ฒด ์ฝ๋**

```html
<!-- ๋ ๊ฐ์ง์ ์ฆ๊ฐ์ ๋ฒํผ์ ํตํด span์ ๊ฐ์ ๋ณ๊ฒฝํ๋ ํ๋ก๊ทธ๋จ -->
<body>
  <button id="add">Add</button>
  <span></span>
  <button id="minus">Minus</button>
</body>
```

```js
// createStore : store ์์ฑ ํจ์
import { createStore } from "redux";

const add = document.getElementById("add");
const minus = document.getElementById("minus");
const number = document.querySelector("span");

number.innerText = 0;

// action : reducer์ ์ํตํ๋ ๋ฐฉ์
// action type์ ๋ณ์ํ ์์ผ ์ค๋ฅ๋ฅผ ์ฝ๊ฒ ์ก์ ์ ์๊ฒ ๋ง๋ฆ
// ์ผ๋ฐ string ํ์์ JS๊ฐ ์ค๋ฅ๋ฅผ ์ก์ง ๋ชปํจ
const ADD = "ADD";
const MINUS = "MINUS";

// reducer : data ์์  ํจ์
// ๋ฐ์ดํฐ๋ฅผ ์ ์ผํ๊ฒ ์์ ํ  ์ ์๋ ๊ณณ
// return ๊ฐ์ application์ data๊ฐ ๋จ
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

// store : date ์ ์ฅ ๊ณต๊ฐ
const countStore = createStore(countModifier);

// store์ ํ์ฌ ์ํ๋ฅผ number์ ์ ์ฅํจ
const onChange = () => {
  number.innerText = countStore.getState();
};

// subscribe : store์ ๋ณํ๋ฅผ ๊ฐ์งํ๋ฉด ์ธ์ ๊ฐ์ผ๋ก ์ค ํจ์๋ฅผ ์คํ
countStore.subscribe(onChange);

// dispatch : reducer์ action์ ๋ณด๋ด๊ณ  ํธ์ถํจ
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};

const handleMinus = () => {
  countStore.dispatch({ type: MINUS });
};

add.addEventListener("click", handleAdd);
minus.addEventListener("click", handleMinus);
```
