---
layout: post
title:  "Binary Search"
date:   2022-09-20 22:46:00 +0900
categories: TIL
---
# Binary Search
오늘 백준 문제를 풀면서 Binary Search를 사용해야 하는 문제를 몇가지 풀었다. 지난 학기 전산학개론 시간에 들어본 것 같긴 한데 직접 코드로 짜보려니 생각만큼 쉽지는 않았다.  

## 수 찾기
N개의 정수 A[1], A[2], …, A[N]이 주어져 있을 때, 이 안에 X라는 정수가 존재하는지 알아내는 프로그램을 작성하시오.  

```python
import sys
input = sys.stdin.readline
N=int(input())
A=list(map(int,input().split()))
M=int(input())
C=list(map(int,input().split()))

for x in C:
  if x in A:
    print(1)
  else:
    print(0)
```
처음에는 당연히 in을 사용하여 다음과 같은 코드를 작성하였다. 하지만 오늘 지겹도록 본 글자인 시간 초과가 나와서 Binary Search를 사용해 다시 풀어보았다.

```python
import sys
input = sys.stdin.readline

def BS(arr,target):
  start=0
  end=len(arr)-1
  while start<=end:
    cen=(start+end)//2
    if arr[cen]==target:
      return 1
    elif arr[cen]<target:
      start=cen+1
    else:
      end=cen-1
  return 0
 
  

N=int(input())
A=list(map(int,input().split()))
A.sort()
M=int(input())
C=list(map(int,input().split()))

for x in C:
  if BS(A,x)==1:
    print(1)
  else:
    print(0)
```
처음에는 단순히 Linear Search 하는 것이 시간복잡도가 O(n)이기 때문에 sort를 먼저하고 Binary Search하는 것보다 빠를 것 같다는 생각이 있었는데 놀랍게도 후자가 더 빠르다고 한다.
참고로 python에서 sort()를 이용하면 시간복잡도가 O(nlogn)인 tim sort를 이용한다고 한다.  


## 숫자 카드 2
숫자 카드는 정수 하나가 적혀져 있는 카드이다. 상근이는 숫자 카드 N개를 가지고 있다. 정수 M개가 주어졌을 때, 이 수가 적혀있는 숫자 카드를 상근이가 몇 개 가지고 있는지 구하는 프로그램을 작성하시오.  

```python
import sys
input = sys.stdin.readline

N=int(input())
card=list(map(int,input().split()))
M=int(input())
num=list(map(int,input().split()))
for i in num:
  count=0
  for j in card:
    if i==j:
      count+=1
  print(count,end=' ')
```
이번에도 처음엔 가장 단순한 방식인 Linear Search로 접근해서 코드를 작성했고 당연하게도 시간초과라는 결과를 얻었다. 

```python
import sys
input = sys.stdin.readline

def BS(arr,target):
  start=0
  end=len(arr)-1
  while start<=end:
    cen=(start+end)//2
    if arr[cen]==target:
      return cen
    elif arr[cen]<target:
      start=cen+1
    else:
      end=cen-1
  return -1

N=int(input())
card=list(map(int,input().split()))
card.sort()
M=int(input())
num=list(map(int,input().split()))

for x in num:
  count=0
  lenth=len(card)-1
  index=BS(card,x)
  while card[index-1]==x and index>0:
    index-=1
    
  while card[index]==x and index<lenth:
    index+=1
    count+=1
  if card[index]==x and index==lenth:
    count+=1
  print(count,end=' ')
```
앞의 문제에서 사용한던 Binary Search를 이용해서 나름 창의적으로 코드를 작성해 봤는데 또다시 시간초과가 나왔다. 정시개 수업에 메모장도 없이 index 계산한다고 고생했는데 짜증나서 잠시 구글의 힘을 빌려보았다.  

```python
import sys
from bisect import bisect_left, bisect_right

input = sys.stdin.readline

N=int(input())
card=list(map(int,input().split()))
card.sort()
M=int(input())
num=list(map(int,input().split()))

def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index


for i in range(len(num)):
    print(count_by_range(card, num[i], num[i]), end=' ')
```
놀랍게도 python에서는 Binary Search에 대한 모듈도 제공하고 있다고 한다. 그리고 직접 코드를 작성해 함수를 선언하고 사용하는 것보다 제공되는 모듈을 이용하는 것이 최적화가 잘 되어 있기 때문에 더 빠르다고 한다. 따라서 공부 목적 이외에 실제로 빠른 코드를 위해서는 제공되는 모듈을 잘 이용해서 프로그램을 작성해야한다.