# 💡 JSX

---

React에서 사용하는 JavaScript의 문법, Html과 Javascript를 모두 사용할 수 있음

# 💡 JSX 사용시 주의할 점

---

### 1\. JSX는 무조건 태그를 닫아줘야함

- <br /> 태그도 예외 없음

### 2\. 두개이상의 태그는 꼭 다른 태그로 감싸줘야 함

- <> 플래그먼트 태그도 가능

### 3\. 리액트에서 JavaScript 문법을 사용하고 싶다면 중괄호를 사용해주기

```
const name = 'react';

<> // 플래그먼트를 활용
<div>name</div>    // 결과창에 name 그대로 나옴
<div>{name}</div>  // 결과창에 name의 값인 react가 나옴
</>
```

### 4\. 스타일 사용시 객체가 필요함

```
const style = {
	backgrondColor : black; // background-color는 - 빼고 대문자로 작성
}
return (
	<div style={style}>
		<div className="my-style">
		</div>
	</div>
)
```

### 5\. 주석

```
return (
	<div>
		{/*주석*/}
		<input
			//주석
		/>
	</div>
)
```
