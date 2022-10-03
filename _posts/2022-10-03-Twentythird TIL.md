---
layout: post
title:  "순열 알고리즘"
date:   2022-10-03 23:14:00 +0900
categories: TIL
---

최근 건강이슈를 비롯해 각종 문제들로 인해 오랜 기간동안 TIL을 작성하지 못했었다. 그래서 오늘에서야 TIL을 쓰려고 뒤늦게 공부를 시작했는데 벌써 많은 기억이 휘발된 것 같다.  
우선 C++과제부터 시도해 보았는데 갑자기 올라간 난이도가 순간 머리가 다시 어질어질해졌다. 우리 구츠너 교수님께 특별히 배운 것도 없는 거 같은데 갑자기 이렇게 과제를 낸 것에 대해 배신감이 들었다.
그중 C++과제 2번에 있는 순열 알고리즘을 공부해보았는데 우선 C++대신 좀 더 친숙한 python을 이용해 알고리즘이 어떻게 돌아가는지 이해하려고 노력했다.

```python
def permutation(arr, r):
    arr = sorted(arr)
    used = [0 for _ in range(len(arr))]

    def generate(chosen, used):
        if len(chosen) == r:
            print(chosen)
            return

        for i in range(len(arr)):
            if used[i]==0:
                chosen.append(arr[i])
                used[i] = 1
                generate(chosen, used)
                used[i] = 0
                chosen.pop()
    generate([], used)
```
이렇게 위와 같은 재귀를 이용하는 방법과 아래에 설명할 반복문을 이용한 방식이 있었는데 솔직히 말하면 두가지 방식 모두 굉장히 마음에 들지 않았다.  
우선 위의 알고리즘을 머리 속으로 따라가다보면 반복문 속 재귀에 재귀에 다시 반복문 속 재귀로 이어지다 재귀 몇개 빠져나가고 다시 재귀가 나오는 엄청난 일이 일어나고 있었다.  
도대체 어떻게 이렇게 알고리즘을 짤 생각을 할 수 있는지 머릿속이 궁금해지는데 이 20줄도 안되는 코드를 이해하는 게 내 머리로는 버거울 듯 했다.  
진짜 알고리즘을 이따위로 짜야되나 싶은 생각이 들면서 벽을 느낄 때쯤 재귀를 이용하지 않는다는 혹하는 코드를 발견했다.

```python
def permute(arr):
    result = [arr[:]]
    c = [0] * len(arr)
    i = 0
    while i < len(arr):
        if c[i] < i:
            if i % 2 == 0:
                arr[0], arr[i] = arr[i], arr[0]
            else:
                arr[c[i]], arr[i] = arr[i], arr[c[i]]
            result.append(arr[:])
            c[i] += 1
            i = 0
        else:
            c[i] = 0
            i += 1
    return result
```
이 코드를 보고 어라 좀 더 나은 것 같은데 라고 생각한 내가 부끄러워질 정도로 1도 이해하지 못하겠다. 진짜 순열 알고리즘은 이렇게 내가 이해하지 못하는 방식으로 코드를 짤 수 밖에 없는지 모르겠다.
오늘 밤을 새서라도 내가 이해할 수 있는 순열 알고리즘 코드를 직접 작성해 볼 생각인데 쉽지 않은 여정이 될 것 같다.