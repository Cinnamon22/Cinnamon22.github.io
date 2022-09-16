---
layout: post
title:  "백준 3제"
date:   2022-09-16 20:13:00 +0900
categories: TIL
---
# 백준 문제 풀이
## 소수 찾기
주어진 수 N개 중에서 소수가 몇 개인지 찾아서 출력하는 프로그램을 작성하시오.  

```python
def Prime(x):
  if x==1:
    return 0
  if x==2:
    return 1
  count=0
  for i in range(2,x):
    if x%i==0:
      count+=1
  if count==0:
    return 1
  else:
    return 0

N=int(input())
L=list(map(int,input().split()))
C=0
for i in L:
  if Prime(i)==1:
    C+=1
print(C)
```
소수인지 판별하는 함수를 작성하고 이를 이용해서 easy하게 풀었다.  

***

## 덩치
우리는 사람의 덩치를 키와 몸무게, 이 두 개의 값으로 표현하여 그 등수를 매겨보려고 한다. 어떤 사람의 몸무게가 x kg이고 키가 y cm라면 이 사람의 덩치는 (x, y)로 표시된다. 두 사람 A 와 B의 덩치가 각각 (x, y), (p, q)라고 할 때 x > p 그리고 y > q 이라면 우리는 A의 덩치가 B의 덩치보다 "더 크다"고 말한다. 예를 들어 어떤 A, B 두 사람의 덩치가 각각 (56, 177), (45, 165) 라고 한다면 A의 덩치가 B보다 큰 셈이 된다. 그런데 서로 다른 덩치끼리 크기를 정할 수 없는 경우도 있다. 예를 들어 두 사람 C와 D의 덩치가 각각 (45, 181), (55, 173)이라면 몸무게는 D가 C보다 더 무겁고, 키는 C가 더 크므로, "덩치"로만 볼 때 C와 D는 누구도 상대방보다 더 크다고 말할 수 없다.  

N명의 집단에서 각 사람의 덩치 등수는 자신보다 더 "큰 덩치"의 사람의 수로 정해진다. 만일 자신보다 더 큰 덩치의 사람이 k명이라면 그 사람의 덩치 등수는 k+1이 된다. 이렇게 등수를 결정하면 같은 덩치 등수를 가진 사람은 여러 명도 가능하다. 아래는 5명으로 이루어진 집단에서 각 사람의 덩치와 그 등수가 표시된 표이다.  

이름	(몸무게, 키)	덩치 등수  
A	(55, 185)	2  
B	(58, 183)	2  
C	(88, 186)	1  
D	(60, 175)	2  
E	(46, 155)	5  
위 표에서 C보다 더 큰 덩치의 사람이 없으므로 C는 1등이 된다. 그리고 A, B, D 각각의 덩치보다 큰 사람은 C뿐이므로 이들은 모두 2등이 된다. 그리고 E보다 큰 덩치는 A, B, C, D 이렇게 4명이므로 E의 덩치는 5등이 된다. 위 경우에 3등과 4등은 존재하지 않는다. 여러분은 학생 N명의 몸무게와 키가 담긴 입력을 읽어서 각 사람의 덩치 등수를 계산하여 출력해야 한다.  

```python
N = int(input())
P = []
for x in range(N):
    P.append(list(map(int, input().split())))

S = sorted(P, key=lambda i: i[0], reverse=True)
R = []
count=1
same=0


for x in range(N-1):
    if S[x][1] > S[x + 1][1]:
        R.append(count)
        count+=same
        count += 1
        same = 0
    else:
        R.append(count)
        same += 1
      
R.append(count)
answer=[]
for x in range(N):
  answer.append(R[S.index(P[x])])
for x in range(N):
  print(answer[x],end=' ')
```
위의 코드는 먼저 몸무게 순서대로 내림차순 정렬을 하고 각각 뒤에 있는 키와 비교해서 클 경우와 작을 경우를 나누어서 작성했다. 예제로 주어진 입력값은 제대로 맞게 출력되었지만 몸무게가 같은 경우와 키가 같은 경우를 고려하지 못해서 틀렸다. 접근방식이 아예 잘못되어서 문제를 다시 처음부터 풀어야해서 분했다.

```python
N = int(input())
P = []
for x in range(N):
    P.append(list(map(int, input().split())))
for i in P:
    rank = 1
    for j in P:
        if i[0] < j[0] and i[1] < j[1]: 
            rank+=1 
    print(rank, end = " ")
```
도저히 어떻게 접근해야할지 떠오르지 않아서 구글의 힘을 빌렸는데 훨씬 짧고 간단하게 풀리는 것을 보고 접근방식이 중요하다는 것을 다시 한번 실감했다. 특히 C언어 for문에 익숙해져서 _list_ 를 i에 대입하는 방식은 생각하지도 못했는데 의식적으로 사용하려고 노력해야겠다.

***
# 좌표 정렬하기 2
2차원 평면 위의 점 N개가 주어진다. 좌표를 y좌표가 증가하는 순으로, y좌표가 같으면 x좌표가 증가하는 순서로 정렬한 다음 출력하는 프로그램을 작성하시오.  

```python
N=int(input())
point=[]
for x in range(N):
  point.append(list(map(int,input().split())))

point.sort(key=lambda i :(i[1],i[0]))
for x in point:
  print(x[0],x[1])
```
위에 덩치 문제를 풀면서 sort나 for문을 여러가지 시도해본 것이 효과가 있었는지 정렬하는 문제는 간단하게 풀 수 있었다.

***
내일은 주말을 맞아 웹프로그래밍을 시작해 보도록 하겠다.