### **문제 조건과 설명**

"OOXXOXXOOO"와 같은 OX퀴즈의 결과가 있다. O는 문제를 맞은 것이고, X는 문제를 틀린 것이다. 문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다. 예를 들어, 10번 문제의 점수는 3이 된다.

"OOXXOXXOOO"의 점수는 1+2+0+0+1+0+0+1+2+3 = 10점이다.

OX퀴즈의 결과가 주어졌을 때, 점수를 구하는 프로그램을 작성하시오.

---

### **Input**

첫째 줄에 테스트 케이스의 개수가 주어진다. 각 테스트 케이스는 한 줄로 이루어져 있고, 길이가 0보다 크고 80보다 작은 문자열이 주어진다. 문자열은 O와 X만으로 이루어져 있다.

---

### **Output**

각 테스트 케이스마다 점수를 출력한다.

---

### **스스로 생각하기**

첫째줄에 테스트 개수인 t를 입력받습니다.

t의 값만큼 테스트를 받아야 하기 때문에 range를 t로 설정해준 뒤 반복문을 정의합니다.

ox라는 변수를 통해 결과를 받아오고 ox를 리스트에 저장합니다.

총 점수의 합을 sum, sum에 더할 값을 저장해줄 cnt를 각각 0으로 초기화합니다.

결과의 점수를 계산하기 위해 두번째 반복문을 정의합니다.

조건문을 통해 입력받은 결과가 O이라면 cnt를 1씩 증가 시킨 뒤 sum에 저장합니다.

예제를 보면 '문제를 맞은 경우 그 문제의 점수는 그 문제까지 연속된 O의 개수가 된다.'라고 했기 때문에

반복문이 X를 만나기 전까진 cnt의 값이 계속 1씩 증가해야합니다.

만약 반복문이 X를 만났다면 O의 연속이 끝났음으로 cnt를 다시 0으로 정의합니다.

마지막으로 점수의 총합인 sum을 출력해줍니다.

**❓ if j == 'O'에서 ox\[j\]가 아닌 j라고 써준 이유**

반복문의 조건에서 j는 ox로 정의됩니다.

파이썬의 특징상 조건을 문자열인 ox로 정의했을 경우, j는 문자 하나하나의 값을 의미합니다.

ox = \['o', 'x', 'x'\]라면 j는 'o' 하나로 정의됩니다.

그러므로 ox\[j\]가 아닌 j 그 자체로 사용해주어야 합니다.

---

### **소스코드**

```
t = int(input())  # 테스트 개수

for i in range(t):
    ox = input()
    list(ox)

    sum = 0
    cnt = 0
    for j in ox:
        if j == 'O':  # 맞은 문제일 때
            cnt += 1
            sum += cnt
        else:  # 틀린 문제일 때
            cnt = 0

    print(sum)
```
