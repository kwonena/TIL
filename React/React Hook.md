# ๐ก React Hook

---

ํจ์ํ ์ปดํฌ๋ํธ์์๋ ํด๋์คํ ์ปดํฌ๋ํธ์ ๊ธฐ๋ฅ์ ์ธ ์ ์๊ฒ๋ ๋ง๋ค์ด์ง ๊ธฐ์ ์ด๋ค. ๊ธฐ์กด ํจ์ํ ์ปดํฌ๋ํธ์์๋ ์ฌ์ฉํ  ์ ์์๋ ์ํ ๊ด๋ฆฌ, Lifecylce ๋ฉ์๋๋ฑ์ ์ฌ์ฉํ  ์ ์๋ค.

# ๐ก ์ฌ์ฉ ๋ฐฉ๋ฒ

---

๊ธฐ๋ณธ์ ์ผ๋ก React Hook์ useStateํจ์๋ฅผ ํตํด state๋ฅผ ํธ์ถํ์ฌ ์ํ ๊ด๋ฆฌ๋ฅผ ํ๋ค. ์ฌ์ฉํ  ๋ณ์์ ๊ทธ ๋ณ์์ ์ํ ๊ด๋ฆฌ๋ฅผ ํด์ค ํจ์๋ฅผ ํธ์ถํ๊ณ  useStateํจ์์์ ๊ธฐ๋ณธ๊ฐ์ ์ค์ ํด ์ฌ์ฉํ๋ค.

num๊ณผ setNum ๋๊ฐ๋ฅผ ์ ์ธํ ํ useState๋ฅผ ํธ์ถํ๊ฒ ๋๋ฉด ๋ฆฌ์กํธ์์ ์ค์  state๊ฐ์ธ num๊ณผ num์ ์๋ฐ์ดํธ ํด์ค ์ ์๋ ํจ์ setNum ๋๊ฐ์ง๋ฅผ return ํด์ค๋ค.

```
import React, { useState } from 'react'; //useState ํจ์ ์ฌ์ฉ ์ ์ธ

function Counter() {
    const [num, setNum] = useState(0);
		//์ฌ์ฉํ  num์ ๊ธฐ๋ณธ๊ฐ์ 0, num์ ๋ฐ๊ฟ์ฃผ๋ setNum ํจ์

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

๋ง์ฐฌ๊ฐ์ง๋ก ํจ์ํ ์ปดํฌ๋ํธ์ด๊ธฐ ๋๋ฌธ์ ์ฝ๋ ์์ ์๋ props๋ state, ์ง์ญ๋ณ์๋ค์ด ๊ณ์ **๋ฐ๋ณต์ ์ผ๋ก ํธ์ถ**๋๋ค.

### โ ๊ณ์ ํธ์ถ๋๋ฉด useState๊ฐ 0์ผ๋ก ์ด๊ธฐํ ๋์ง ์์๊น?

useState๋ ๋ฆฌ์กํธ ํ์์ ์ ๊ณตํ๋ API ์ค์ ํ๋๋ก useState๋ฅผ ์ฌ์ฉํ๋ฉด ๋ฆฌ์กํธ๊ฐ ์๋์ผ๋ก ๊ธฐ์ตํ๊ณ  ์๋ค. ๊ทธ๋์ ์ด๊ธฐํ ๋์ง ์๊ณ  ๋์ผํ ๊ฐ์ ๋ฐ์์ฌ ์ ์๋ค.

# ๐ก Ref๋ฅผ ์ฌ์ฉํ  ๋

---

๊ธฐ์กด **ํด๋์คํ ์ปดํฌ๋ํธ**์์ Ref๋ฅผ ์ฌ์ฉํ  ๋ createRef() ํจ์๋ฅผ ์ด์ฉํ๋ค.

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

ํ์ง๋ง state๊ฐ ๋ณ๊ฒฝ๋  ๋๋ง๋ค ์ฝ๋๋ธ๋ญ์ด ๊ณ์ํด์ ์คํ๋๋ **ํจ์ํ ์ปดํฌ๋ํธ**์์๋ Ref๋ฅผ ๋ฐ๋ณต์ ์ผ๋ก ๋ง๋ค์ง ์๊ธฐ ์ํด์ ๋ฆฌ์กํธ ํ์์ ์ ๊ณตํ๋ **useRef()** ํจ์๋ฅผ ์ฌ์ฉํ๋ค. ๋งค๋ฒ ์๋ก์ด ๋ ํผ๋ฐ์ค๋ฅผ ๋ง๋ค์ง ์๊ณ  ํ ๋ฒ ๋ง๋  ๊ฒ์ ์ฌ์ฌ์ฉํ  ์ ์๊ฒ ํด์ค๋ค.

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

# ๐ก Lifecylce ํจ์ ์ฌ์ฉํ๊ธฐ

---

๋ฆฌ์กํธ ํ์ ์ฌ์ฉํ๋ฉด ํจ์ํ ์ปดํฌ๋ํธ์์๋ **Lifecylce ํจ์**๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.

ํด๋์คํ ์ปดํฌ๋ํธ์์๋ componentDidMount()์ componentDidUpdate() ๋๊ฐ์ง๊ฐ ํ์ํ  ๋ ์ฝ๋๋ฅผ ์ค๋ณตํด์ ๋๊ฐ์ง๋ฅผ ๋ชจ๋ ํธ์ถํ๋ ๊ฒฝ์ฐ๊ฐ ์๋ค.

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

๋ฆฌ์กํธ ํ์์๋ ํด๋์คํ ์ปดํฌ๋ํธ์ ์ด๋ฌํ ์ ์ ๋ณด์ํ์ฌ componentDidMount()์ componentDidUpdate() ๋ ๊ฐ์ ํจ์๋ฅผ \*\*useEffect()\*\*๋ผ๋ ํจ์๋ฅผ ํตํด ํ ๋ฒ๋ง ์ ์ํด์ ์ฌ์ฉํ  ์ ์๊ฒ ํด์ค๋ค.

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

์ปดํฌ๋ํธ๊ฐ ์๋ฐ์ดํธ ๋  ๋๋ง๋ค ํจ์๋ฅผ ๋ถ๋ฌ์ค๋ ๊ฒ์ด ์๋ ์ด๋ค ๊ฐ์ด ๋ณ๊ฒฝ๋์ด **ํ์ํ  ๋๋ง ํธ์ถ**ํ  ์ ์๋๋ก ๋ง๋๋ ๊ฒ์ด ๋ ์ ์ฉํ๋ค.

```
useEffect(() => {
    console.log('mounted & updated!');
}, [count]);
```

useEffect()์ ๋ณ์๋ฅผ ์ ๋ฌํ๋ฉด ๋ณ์๊ฐ ๋ณ๊ฒฝ๋  ๋๋ง ํธ์ถํ๊ฒ ํ  ์ ์๋ค.
