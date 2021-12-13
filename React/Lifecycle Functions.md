# 💡 Lifecycle 함수

---

component가 만들어지거나 브라우저 상에서 표기 될 때 수행해야 하는 일들을 처리할 수 있게 해주는 함수로 '생명주기 메소드'라고 불리운다.

component 클래스를 상속한다면 Lifecycle 메소드를 사용할 수 있게 된다.

[##_Image|kage@lJPyv/btrlEn7UclV/jXMpseX0p9GMkiUxOrKD70/img.png|CDM|1.3|{"originWidth":499,"originHeight":292,"style":"alignCenter","filename":"Untitled.png"}_##]

component의 여러 상황에서 쓸 수 있는 함수들이며 구현시 리액트가 **자동으로** 함수를 호출해준다.

### 주로 사용하는 Lifecylcle 함수들

- **componentDidMount()**

component가 UI상에 등록되어 사용자에게 보여질 때 호출됨

- **componentWillUnmount()**

component를 UI상에서 삭제하기 전에 호출됨

- **componentDidUpdate()**

component의 정보가 업데이트 될 때 호출되며 최초 렌더링시에는 호출되지 않음
