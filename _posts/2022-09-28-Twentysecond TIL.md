---
layout: post
title:  "DP"
date:   2022-09-29 00:06:00 +0900
categories: TIL
---
# DP
DP라고 하면 탈영병 잡는 넷플릭스 드라마가 먼저 생각나지만 오늘 소개할 DP는 __Dynamic Programming__ 이라는 동적 프로그래밍에 대한 내용이다. 며칠 전 백준 몇 문제를 둘러보다가 하나같이 어떻게 풀어야 될지 모르는 상황에 빠졌다. 그래서 이것 저것 찾아보니 DP에 대해 공부해보라는 말이 많이 보여서 DP에 대해 알아보았다. 우정이 형이 보내준 알고리즘 책을 이용해서 DP를 먼저 공부했는데 DP란 큰 문제를 작은 문제로 나누어서 풀이하는 프로그래밍을 말한다. 가장 보편적인 예시는 피보나치 수열에 대한 것인데 이미 한 번 계산 된 값을 저장해두고 다음 번에 활용하는 방식이다.  
DP는 크게 Top-Down 방식과 Bottom-up 방식이 있는데 다음 문제를 보면서 함께 알아보자.

***


## 1로 만들기
정수 X에 사용할 수 있는 연산은 다음과 같이 세 가지 이다.  

X가 3으로 나누어 떨어지면, 3으로 나눈다.  
X가 2로 나누어 떨어지면, 2로 나눈다.  
1을 뺀다.  
정수 N이 주어졌을 때, 위와 같은 연산 세 개를 적절히 사용해서 1을 만들려고 한다. 연산을 사용하는 횟수의 최솟값을 출력하시오.  

  
다음과 같은 문제가 주어지면 가장 먼저 생각할 수 있는 것은 모든 경우의 수를 모두 계산하는 방식인 브루투 포스이다. 하지만 3가지의 경우를 순서를 바꿔가며 모두 계산하려면 조금만 수가 커져도 불가능에 가까운 경우의 수가 나온다. DP에서 가장 핵심이 되는 개념은 점화식이다. 예전 고등학교 수학에서 배운적이 있는 것 같은데 피보나치 수열의 경우 __F(n)=F(n-1)+F(n-2)__라는 식이 점화식이다.
이번 1로 만들기의 점화식은 __F(n)=min(F(n-1)+1,F(n//2)+1,F(n//3)+1)__ (물론 2와 3으로 나누어지는 것이 가능해야한다.) 이다.

```python
def make_one(n,memo):
  if n in memo:
    return memo[n]
  if n%2==0 and n%3==0:
    memo[n]=min(make_one(n//2,memo)+1,make_one(n//3,memo)+1)
  elif n%2==0:
    memo[n]=min(make_one(n-1,memo)+1,make_one(n//2,memo)+1)
  elif n%3==0:
    memo[n]=min(make_one(n-1,memo)+1,make_one(n//3,memo)+1)
  else:
    memo[n]=make_one(n-1,memo)+1
  return memo[n]

N=int(input())
memo={1:0}
print(make_one(N,memo))
```
위의 코드가 Top-Down 방식을 활용해서 작성한 코드인데 Recursion(재귀)를 사용하기 때문에 잘못 작성하면 메모리가 터지는 경우가 많다. 나도 처음 코드를 작성할 때 딕셔너리 대신 리스트를 이용해 코드를 작성했다가 메모리 초과의 늪에 빠진 경험이 있다. 하지만 Bottom-Up 방식에 비해 필요한 부분의 값만 계산하면 되기 때문에 상대적으로 유리한 경우도 존재한다고 하는데 메모리 초과와 Recursive 오류의 늪에 빠질 수 있기 때문에 꼭 필요한 경우가 아니면 다른 방법을 생각하는 것도 좋을 것 같다.

```python
N=int(input())
if N<4:
    memo=[-1]*5
else :
    memo=[-1]*(N+1)
memo[1]=0
memo[2]=1
memo[3]=1
memo[4]=2
def make_one(n):
  global memo
  for x in range(5,n+1):
    if x%2==0 and x%3==0:
      memo[x]=min(memo[x-1]+1,memo[x//2]+1,memo[x//3]+1)
    elif x%2==0:
      memo[x]=min(memo[x-1]+1,memo[x//2]+1)
    elif x%3==0:
      memo[x]=min(memo[x-1]+1,memo[x//3]+1)
    else:
      memo[x]=memo[x-1]+1
  return memo[n]

print(make_one(N))
```
이 코드는 Bottom-Up 방식을 이용해 코드를 작성한 것인데 Recursion이 없다는 점에서 마음이 편안해진다. 하지만 1에서 부터 N까지 차례로 계산해 나가기 때문에 상대적으로 시간이 오래 걸릴 수 있는 단점이 있긴 하다. for 반복문을 활용해서 값을 계산하고 memo라는 리스트에 값을 넣어 저장해 두었다 다음에 필요할 때 활용하는 방식이다.  
알고리즘 그냥 생각나는대로 풀면 되는 줄 알았는데 공부하고 풀어야 된다는 것을 최근에 깨닫고 있다. 공부할 건 많은데 공부하기 싫다ㅠ