# ๐ก Component๋?

---

์ฌ์ฌ์ฉ์ด ๊ฐ๋ฅํ๊ฒ๋ ๋ง๋  **๋๋ฆฝ์ ์ธ UI ์กฐ๊ฐ**์ด๊ณ  ๋ฆฌ์กํธ์์ ์ฌ์ฉํ๋ ์ต์ํ์ ๋จ์์ด๋ค.

# ๐ก Component์ ์ข๋ฅ

---

### Class component

- Component
- Purecomponent

### Function component

- Function
- memo (Higher Order Component)
- React Hook

# ๐ก Component์ ๊ธฐ๋ณธ ๊ตฌ์กฐ

---

### โ Class Component

- ๋ฆฌ์กํธ์์ ์ ๊ณตํ๋ component class๋ฅผ ์์ํด์ ๋ง๋ ๋ค.
- component์ state(object)๊ฐ **ํ์**ํ๋ฉฐ ์ฃผ๊ธฐ์ ์ผ๋ก ์๋ฐ์ดํธ ๋  ๋ ์ฌ์ฉํ๋ค.
- state๊ฐ ๋ณ๊ฒฝ๋  ๋ component๋ render ํจ์๋ฅผ ํธ์ถํ๋ฉฐ ์ฌ์ฉ์์๊ฒ ์๋ฐ์ดํธ ๋ ๋ด์ฉ์ ๋ณด์ฌ์ค๋ค.
- Life cycle ๋ฉ์๋๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
- ๋ฉค๋ฒ๋ณ์์ ์ ๊ทผํ  ๋ ํญ์ this๋ฅผ ๋ถ์ฌ ์ ๊ทผํด์ผ ํ๋ค.

```
import React, { Component } from 'react';

class Test extends Component {
  showTestMessage = () => {
    console.log("Hello:)");
  }
  render() {
    return <button onClick={this.showTestMessage}>Clickโ</button>
  }
}

export default Test;
```

ํด๋์คํ ์ปดํฌ๋ํธ์ ๊ธฐ๋ณธ ๊ตฌ์กฐ

### โ Function Component

- ๊ฐ๋จํ๊ฒ ํจ์๋ก ๋ง๋ค ์ ์๋ component์ด๋ค
- state๋ Life cycle ๋ฉ์๋๊ฐ **ํ์์๊ณ ** ์ ์ ์ผ๋ก ๋ฐ์ดํฐ๊ฐ ํ๊ธฐ ๋  ๋ ์ฌ์ฉํ๋ค.
- React Hook์ ์ฌ์ฉํ๋ฉด Function Component์์๋ state๋ Life cycle ๋ฉ์๋๋ฅผ ์ฌ์ฉํ  ์ ์๋ค.
- const๋ก ์ง์ญ๋ณ์๋ฅผ ํ ๋นํ๋ฉฐ this๋ฅผ ์ฌ์ฉํ์ง ์์๋ ๋๋ค.

```
import React from 'react';

function Test(props) {
  const showTestMessage = () => {
    console.log("Hello:)");
  }
  return <button onClick={showTestMessage}>Clickโ</button>
};

export default Test;
```

ํจ์ํ ์ปดํฌ๋ํธ์ ๊ธฐ๋ณธ ๊ตฌ์กฐ
