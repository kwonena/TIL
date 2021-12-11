# 💡 Shallow comparison

---

리액트가 사용하는 shallow comparison은 오브젝트의 레퍼런스를 비교하는 것이다. 오브젝트가 가지고 있는 내부 안에서 **데이터가 어떻게 변경되는지는 상관하지 않고 동일한 레퍼런스를 가지고 있는 오브젝트일때** true를 반환하며, 동일한 오브젝트라고 판단해 **render 함수를 호출하지 않는다.**

- **reference는 변경되지 않고, data만 변경 되었기 때문에 동일한 오브젝트라고 판단**
- → render 함수 호출X

```
// true
let person = [ // reference : data, person은 오브젝트
{
    name : **"ena"**,
  age : 24,
}

let person = [
{
    name : **"nana"**,
  age : 24,
}
```

- **reference가 변경 되었기 때문에 다른 오브젝트라고 판단**
- → render 함수 호출O

```
// false
let person = [
{
    **name** : "ena",
  age : 24,
}

let person = [
{
    **team** : "ena",
  age : 24,
}
```
