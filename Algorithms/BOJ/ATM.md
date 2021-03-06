### **문제 조건과 설명**

인하은행에는 ATM이 1대밖에 없다. 지금 이 ATM앞에 N명의 사람들이 줄을 서있다. 사람은 1번부터 N번까지 번호가 매겨져 있으며, i번 사람이 돈을 인출하는데 걸리는 시간은 Pi분이다.

사람들이 줄을 서는 순서에 따라서, 돈을 인출하는데 필요한 시간의 합이 달라지게 된다. 예를 들어, 총 5명이 있고, P1 \= 3, P2 \= 1, P3 \= 4, P4 \= 3, P5 \= 2 인 경우를 생각해보자. \[1, 2, 3, 4, 5\] 순서로 줄을 선다면, 1번 사람은 3분만에 돈을 뽑을 수 있다. 2번 사람은 1번 사람이 돈을 뽑을 때 까지 기다려야 하기 때문에, 3+1 = 4분이 걸리게 된다. 3번 사람은 1번, 2번 사람이 돈을 뽑을 때까지 기다려야 하기 때문에, 총 3+1+4 = 8분이 필요하게 된다. 4번 사람은 3+1+4+3 = 11분, 5번 사람은 3+1+4+3+2 = 13분이 걸리게 된다. 이 경우에 각 사람이 돈을 인출하는데 필요한 시간의 합은 3+4+8+11+13 = 39분이 된다.

줄을 \[2, 5, 1, 4, 3\] 순서로 줄을 서면, 2번 사람은 1분만에, 5번 사람은 1+2 = 3분, 1번 사람은 1+2+3 = 6분, 4번 사람은 1+2+3+3 = 9분, 3번 사람은 1+2+3+3+4 = 13분이 걸리게 된다. 각 사람이 돈을 인출하는데 필요한 시간의 합은 1+3+6+9+13 = 32분이다. 이 방법보다 더 필요한 시간의 합을 최소로 만들 수는 없다.

줄을 서 있는 사람의 수 N과 각 사람이 돈을 인출하는데 걸리는 시간 Pi가 주어졌을 때, 각 사람이 돈을 인출하는데 필요한 시간의 합의 최솟값을 구하는 프로그램을 작성하시오.

---

### **Input**

첫째 줄에 사람의 수 N(1 ≤ N ≤ 1,000)이 주어진다. 둘째 줄에는 각 사람이 돈을 인출하는데 걸리는 시간 Pi가 주어진다. (1 ≤ Pi ≤ 1,000)

---

### **Output**

첫째 줄에 각 사람이 돈을 인출하는데 필요한 시간의 합의 최솟값을 출력한다.

---

### **스스로 생각하기**

예시에서 최단 시간이 걸리는 경우는

시간이 적게 걸리는 번호대로 줄을 서는 것입니다.

그래서 알고리즘은 시간이 적게 걸리는 순으로 사람들을 배열해

해당 번호의 시간과 그 전 번호의 시간을 합쳐 총 합계를 구하는 것으로 생각했습니다.

n을 입력 받은 후,

사람 별로 돈을 인출하는 시간을 입력 받기 위한 리스트 people을 만들어

sort함수로 정렬해줍니다.

정렬된 people 리스트에서 시간의 합계를 구하기 위해

배열 time을 n의 길이만큼 정의해줍니다.

반복문을 통해 첫번째 인덱스라면 그 인덱스의 값 그대로 time에 할당해주고

첫 번째 인덱스가 아니라면 그 전 time의 인덱스와 해당 인덱스를 더해 time에 할당해줍니다.

time에는 기다린 시간과 자신이 걸리는 시간이

앞의 순서대로 할당 되어 있기 때문에 그 전 time의 인덱스를 더해주면

사람별로 걸리는 시간을 구할 수 있습니다.

마지막으로 time의 총 합계를 sum 함수를 사용해 구하고 출력해줍니다.

---

### **소스코드**

```
n = int(input())

people = list(map(int, input().split()))
people.sort() # 시간 순서대로 정렬

time = [0] * n # 돈을 인출하는데 필요한 시간 배열

for i in range(len(people)):
    if i > 0:
        time[i] = time[i - 1] + people[i]
    else:
        time[i] = people[i]

print(sum(time))
```
