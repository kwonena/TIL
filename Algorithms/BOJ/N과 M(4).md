### **문제 조건과 설명**

자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.

- 1부터 N까지 자연수 중에서 M개를 고른 수열
- 같은 수를 여러 번 골라도 된다.
- 고른 수열은 비내림차순이어야 한다.
  - 길이가 K인 수열 A가 A1 ≤ A2 ≤ ... ≤ AK-1 ≤ AK를 만족하면, 비내림차순이라고 한다.

---

### **Input**

첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)

---

### **Output**

한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.

수열은 사전 순으로 증가하는 순서로 출력해야 한다.

---

### **스스로 생각하기**

N과 M 시리즈의 마지막 문제입니다.

이번 문제는 중복을 허용한 조합입니다.

중복을 허용한 조합에는

combinations_with_replacement 함수를 사용해줍니다.

```
combinations_with_replacement(구하고자 하는 수의 범위, 고를 수의 개수)
```

arr에 combinations_with_replacement의 값을 리스트 형태로 저장하고,

여기서도 출력예제을 보면 한 줄에 하나의 값이 나오는 것을 볼 수 있습니다.

combinations_with_replacement 함수의 출력문은 튜플의 형태로 짝이 지어져 출력됩니다.

**_ex) \[(1, 2), (2, 3)\]_**

출력 양식을 맞추기 위해 반복문으로 i를 통해

arr 리스트 값을 하나씩 받아오고

튜플의 압축을 해제하기 위해 \*를 사용해줍니다.

(✔️ 중복되지만 혼란 방지를 위해 계속 언급하겠습니다ㅎ,,)

---

### **소스코드**

```
from itertools import combinations_with_replacement

n, m = map(int, input().split())

arr = list(combinations_with_replacement(range(1, n + 1), m))

for i in arr:
    print(*i, sep=' ')
```
