# 💡 **To Do 상세 코드**

### ✔ App.js

- react-router-dom package를 사용해 router을 사용한 페이지 이동

```js
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Detail from "./Detail";
import Home from "./Home";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" expact element={<Home />}></Route>
        <Route path="/:id" element={<Detail />}></Route>
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

### ✔ Home.js

- input에 text를 입력하고 입력한 text를 ul에 보여주는 To Do List

```js
import React, { useState } from "react";
import { connect } from "react-redux";
import { actionCreators } from "../routes/store.js";
import ToDo from "./ToDo.js";

function Home({ toDos, addToDo }) {
  const [text, setText] = useState("");

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onSubmit = (e) => {
    e.preventDefault();
    addToDo(text);
    setText("");
  };

  return (
    <>
      <h1>To Do</h1>
      <form onSubmit={onSubmit}>
        <input type="text" value={text} onChange={onChange} />
        <button>Add</button>
      </form>
      <ul>
        {toDos.map((toDo) => (
          <ToDo {...toDo} key={toDo.id} />
        ))}
      </ul>
    </>
  );
}

function mapStateToProps(state) {
  return { toDos: state };
}

function mapDispatchToProps(dispatch) {
  return {
    addToDo: (text) => dispatch(actionCreators.addToDo(text)),
  };
}

export default connect(mapStateToProps, mapDispatchToProps)(Home);
```

- **connect 함수**
  - Home으로 보내는 props에 추가할 수 있도록 허용해줌
  - mapStateToProps와 mapDispatchToProps에서 return한 값이 prop으로 추가됨
  - state와 dispatch에 관련된 함수를 인자로 가짐
  - dispatch 값만 필요한 경우 state 값을 null로 써주는 것이 가능
- **mapStateToProps 함수**
  - connect에 연결된 함수로써 store에서 state를 가져와 주는 함수
  - state 값은 실제로 store에 있는 state값임
  - return값이 필수로 필요함
- **mapDispatchToProps 함수**
  - addToDo 함수가 실행되면 dispatch를 호출
  - store에 있는 actionCreators에 접근해

```js
function mapStateToProps(state) {
  return { toDos: state };
}

function mapDispatchToProps(dispatch) {
  return {
    addToDo: (text) => dispatch(actionCreators.addToDo(text)),
  };
}

export default connect(mapStateToProps, mapDispatchToProps)(Home);
```

### ✔ Detail.js

```js
import React from "react";
import { connect } from "react-redux";
import { useParams } from "react-router-dom";

function Detail({ toDos }) {
  const id = useParams().id;
  // find() : 조건을 만족하는 배열의 첫번째 요소를 반환함
  const toDo = toDos.find((toDo) => toDo.id === parseInt(id));

  return (
    <>
      <h1>{toDo?.text}</h1>
      <h5>Created at: {toDo?.id}</h5>
    </>
  );
}

function mapStateToProps(state) {
  return { toDos: state };
}

export default connect(mapStateToProps)(Detail);
```

- **Optional Chaining(옵셔널 체이닝)**
  - ?.을 사용해 값이 존재하지 않으면 undefined를 반환함
  - 기존의 && 연산자와 비슷한 역할을 하며 코드 수를 줄여줌
  - toDo?.text는 toDo && toDo.text와 같은 용도로 사용됨

```js
<h1>{toDo?.text}</h1>
<h5>Created at: {toDo?.id}</h5>
```

### ✔ ToDo.js

```js
import React from "react";
import { connect } from "react-redux";
import { Link } from "react-router-dom";
import { actionCreators } from "../routes/store";

const ToDo = ({ text, onBtnClick, id }) => {
  return (
    <li>
      <Link to={`/${id}`}>
        {text} <button onClick={onBtnClick}>DEL</button>
      </Link>
    </li>
  );
};

function mapDispatchToProps(dispatch, ownProps) {
  return {
    onBtnClick: () => dispatch(actionCreators.deleteToDo(ownProps.id)),
  };
}

// state값은 필요하지 않은 경우, null로 써줌
export default connect(null, mapDispatchToProps)(ToDo);
```

- **ownProps**
  - mapDispatchToProps의 두번째 인자로 생략 가능
  - 컴포넌트가 현재 가지고 있는 모두 props를 보여줌

# 💡 **전체 코드**

```js
// Directory Structure
root
 └─ src // index
    ├─ components // App, Detail, Home, ToDo
    └─ routes // store
```

```js
// App.js
import React from "react";
import { BrowserRouter, Route, Routes } from "react-router-dom";
import Detail from "./Detail";
import Home from "./Home";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" expact element={<Home />}></Route>
        <Route path="/:id" element={<Detail />}></Route>
      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

```js
// Detail.js
import React from "react";
import { connect } from "react-redux";
import { useParams } from "react-router-dom";

function Detail({ toDos }) {
  const id = useParams().id;
  // find() : 조건을 만족하는 배열의 첫번째 요소를 반환함
  const toDo = toDos.find((toDo) => toDo.id === parseInt(id));

  return (
    <>
      {/* Optional Chaining : ?.을 사용해 값이 존재하지 않으면 undefined를 반환함
      기존의 && 연산자와 비슷한 역할을 하며 코드 수를 줄여줌
      toDo?.text는 toDo && toDo.text와 같은 용도로 사용됨 */}
      <h1>{toDo?.text}</h1>
      <h5>Created at: {toDo?.id}</h5>
    </>
  );
}

function mapStateToProps(state) {
  return { toDos: state };
}

export default connect(mapStateToProps)(Detail);
```

```js
// Home.js
import React, { useState } from "react";
import { connect } from "react-redux";
import { actionCreators } from "../routes/store.js";
import ToDo from "./ToDo.js";

function Home({ toDos, addToDo }) {
  const [text, setText] = useState("");

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onSubmit = (e) => {
    e.preventDefault();
    addToDo(text);
    setText("");
  };

  return (
    <>
      <h1>To Do</h1>
      <form onSubmit={onSubmit}>
        <input type="text" value={text} onChange={onChange} />
        <button>Add</button>
      </form>
      <ul>
        {toDos.map((toDo) => (
          <ToDo {...toDo} key={toDo.id} />
        ))}
      </ul>
    </>
  );
}

// connect에 연결된 함수로써 store에서 state를 가져와 주는 함수
// state 값은 실제로 store에 있는 state값임
// return값이 필수로 필요함
function mapStateToProps(state) {
  return { toDos: state };
}

// addToDo 함수가 실행되면 dispatch를 호출
function mapDispatchToProps(dispatch) {
  return {
    addToDo: (text) => dispatch(actionCreators.addToDo(text)),
  };
}

// connect() : Home으로 보내는 props에 추가할 수 있도록 허용해줌
// mapStateToProps에서 return한 값이 prop으로 추가됨
// state와 dispatch에 관련된 함수를 인자로 가지며 값이 없을 경우 null로 써주는 것이 가능
export default connect(mapStateToProps, mapDispatchToProps)(Home);
```

```js
// ToDo.js
import React from "react";
import { connect } from "react-redux";
import { Link } from "react-router-dom";
import { actionCreators } from "../routes/store";

const ToDo = ({ text, onBtnClick, id }) => {
  return (
    <li>
      <Link to={`/${id}`}>
        {text} <button onClick={onBtnClick}>DEL</button>
      </Link>
    </li>
  );
};

function mapDispatchToProps(dispatch, ownProps) {
  return {
    onBtnClick: () => dispatch(actionCreators.deleteToDo(ownProps.id)),
  };
}

export default connect(null, mapDispatchToProps)(ToDo);
```
