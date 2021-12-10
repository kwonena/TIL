# 💡 Purecomponent

---

**최상위의 데이터가 변경되지 않으면 render 함수를 호출하지 않는 Component**

component가 업데이트 될 때마다 render 함수가 호출되는데 관련 데이터가 변경되지 않았음에도 render 함수를 계속 호출하는 것은 성능에 좋지 않다.

이때 사용하는 방법이 Purecomponent와 memo인데, component에 **state나 props에 변화가 없다면** render 함수가 호출되는 것을 막아주는 것이다.

# 💡 Component와 Purecomponent의 차이점

---

### Component

ShouldComponentUpdate() 구현X

### Purecomponent

ShouldComponentUpdate() 구현O

### ❓ **ShouldComponentUpdate()?**

**Component의 업데이트 여부를 알아보는 함수**

이전 props와 state를 비교 후 업데이트가 필요하면 **true**, 필요하지 않으면 **false**를 리턴해서 Component가 업데이트 될 수 있게 함
