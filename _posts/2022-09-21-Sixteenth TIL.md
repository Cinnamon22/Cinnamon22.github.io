---
layout: post
title:  "Python"
date:   2022-09-20 22:46:00 +0900
categories: TIL
---
# Python
오늘 우연한 기회에 창소프 문제를 얻을 기회가 있어서 python 문제를 풀어보았다.  
생각보다 다양한 부분을 다루고 있었는데 생소한 set나 dictionary 같은 파트도 있어서 구글의 힘을 빌리기도 하였다. 그래도 지금까지 python을 공부한 것이 쓸데가 있기는 한 것 같다는 생각을 했다.  

## 카드2
N장의 카드가 있다. 각각의 카드는 차례로 1부터 N까지의 번호가 붙어 있으며, 1번 카드가 제일 위에, N번 카드가 제일 아래인 상태로 순서대로 카드가 놓여 있다.  

이제 다음과 같은 동작을 카드가 한 장 남을 때까지 반복하게 된다. 우선, 제일 위에 있는 카드를 바닥에 버린다. 그 다음, 제일 위에 있는 카드를 제일 아래에 있는 카드 밑으로 옮긴다.  

예를 들어 N=4인 경우를 생각해 보자. 카드는 제일 위에서부터 1234 의 순서로 놓여있다. 1을 버리면 234가 남는다. 여기서 2를 제일 아래로 옮기면 342가 된다. 3을 버리면 42가 되고, 4를 밑으로 옮기면 24가 된다. 마지막으로 2를 버리고 나면, 남는 카드는 4가 된다.  

N이 주어졌을 때, 제일 마지막에 남게 되는 카드를 구하는 프로그램을 작성하시오.  

```python
N=int(input())
card=list(range(1,N+1))
while(len(card)>1):
  del card[0]
  card.append(card[0])
  del card[0]
print(card[0])
```
처음에는 단순하게 list를 이용해서 코드를 작성했는데 또 다시 시간초과의 늪에 빠졌다.  

```python
import collections
N=int(input())
card=collections.deque(range(1,N+1))
while len(card)>1:
  card.popleft()
  card.rotate(-1)
print(card[0])
```
그래서 알게된 __deque__, list보다 시간복잡도가 빠르기 때문에 스택이나 큐를 활용하는 문제에서 이용해야 한다고 한다. 그래서 이후 푸는 문제에서 deque를 자주 활용하였다.

```cpp
#include <iostream>
int main(){
int N;
int arr[500000];
std::cin>>N;
for(int i=1;i<=N;i++){
  arr[i-1]=i;
}
int head=0;
int rear=N;
int count=0;
while((head+1)%(N+1)!=rear){
  arr[head]=0;
  head=(head+1)%(N+1);
  arr[rear]=arr[head];
  arr[head]=0;
  rear=(rear+1)%(N+1);
  head=(head+1)%(N+1);
  }
std::cout<<arr[head];
  }
```
너무 파이썬만 이용하는 것 같아서 C++로도 풀어보았는데 원형큐를 이용해 작성하였다. 파이썬보다 코드가 복잡하긴 하지만 데이터 구조를 공부하는데 좋은 언어라고 생각했다.