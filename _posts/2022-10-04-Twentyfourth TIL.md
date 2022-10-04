---
layout: post
title:  "계단오르기"
date:   2022-10-04 16:25:00 +0900
categories: TIL
---

지난 연휴동안 건강문제로 하루종일 누워서 잠만 자다보니 밤낮이 완전히 바뀌어버렸다. 오늘도 6시가 넘어서야 겨우 잠에 들어서 3시간정도 밖에 자지 못했는데 확실히 잠을 적게 자니까 사람이 예민해지는 것 같다. 오늘 구츠너 교수님의 풀강을 듣다가 짐을 싸서 뛰쳐나가고 싶은 충동이 들었지만 오늘 말고도 이번주에 출튀할 일이 종종 있을 것 같아 기다렸다. 지금도 정시개를 듣고 있는데 대체 왜 영어전공을 하는 지 이해할 수가 없다. 교수님도 영어를 못하고 나도 영어를 못하는데 대체 누구를 위해서 영어강의를 하는 것인지 모르겠다. 다음주부터는 중간고사를 준비하기 시작해야 될 것 같은데 ppt양이 엄청나다는 소문을 듣고 벌써부터 걱정이 앞선다.  
아무튼 오늘 새벽에 잠이 오지 않아서 풀었던 문제 1개를 소개한다.


***


계단 오르기 게임은 계단 아래 시작점부터 계단 꼭대기에 위치한 도착점까지 가는 게임이다. <그림 1>과 같이 각각의 계단에는 일정한 점수가 쓰여 있는데 계단을 밟으면 그 계단에 쓰여 있는 점수를 얻게 된다.  


![그림 1](https://upload.acmicpc.net/7177ea45-aa8d-4724-b256-7b84832c9b97/-/preview/)
<그림 1>  

예를 들어 <그림 2>와 같이 시작점에서부터 첫 번째, 두 번째, 네 번째, 여섯 번째 계단을 밟아 도착점에 도달하면 총 점수는 10 + 20 + 25 + 20 = 75점이 된다.  


![그림 2](https://upload.acmicpc.net/f00b6121-1c25-492e-9bc0-d96377c586b0/-/preview/)
<그림 2>  

계단 오르는 데는 다음과 같은 규칙이 있다.  

계단은 한 번에 한 계단씩 또는 두 계단씩 오를 수 있다. 즉, 한 계단을 밟으면서 이어서 다음 계단이나, 다음 다음 계단으로 오를 수 있다.  
연속된 세 개의 계단을 모두 밟아서는 안 된다. 단, 시작점은 계단에 포함되지 않는다.  
마지막 도착 계단은 반드시 밟아야 한다.  
따라서 첫 번째 계단을 밟고 이어 두 번째 계단이나, 세 번째 계단으로 오를 수 있다. 하지만, 첫 번째 계단을 밟고 이어 네 번째 계단으로 올라가거나, 첫 번째, 두 번째, 세 번째 계단을 연속해서 모두 밟을 수는 없다.  

각 계단에 쓰여 있는 점수가 주어질 때 이 게임에서 얻을 수 있는 총 점수의 최댓값을 구하는 프로그램을 작성하시오.  

```python
def up_stair(stair,score):
  if stair<=3:
    if stair==1:
      return score[1]
    elif stair==2:
      return (score[1]+score[2])
    elif stair==3:
      return max(score[1]+score[3],score[2]+score[3])
  else:
    return max(up_stair(stair-2,score)+score[stair],up_stair(stair-3,score)+score[stair-1]+score[stair])


stair=int(input())
score=[0]
for x in range(stair):
  score.append(int(input()))

print(up_stair(stair,score))
```
지난번에 설명했던 D.P를 이용해서 푸는 문제인데 생각보다 점화식을 구하는 것이 까다로웠다. 연속으로 3계단을 오르면 안된다는 표현을 어떻게 할 지 고민하여 
__f(x)=max(f(x-2)+score(x),f(x-3)+score(x-1)+score(x))__  (단,x>=4이다) 라는 점화식을 얻을 수 있었다.
위의 방식을 top-down방식으로 코드를 작성하였는데 역시 재귀가 많이 들어가 있다보니 시간초과가 나와서 bottom-up 방식으로 수정하여 다시 작성했다.

```python
def up_stair(stair,score):
  memo=[0]*301
  memo[1]=score[1]
  memo[2]=score[1]+score[2]
  memo[3]=max(score[1]+score[3],score[2]+score[3])
  
  for x in range(4,stair+1):
    memo[x]=max(memo[x-2]+score[x],memo[x-3]+score[x-1]+score[x])
  return memo[stair]

stair=int(input())
score=[0]*301
for x in range(1,stair+1):
  score[x]=int(input())

print(up_stair(stair,score))
```
반복문을 이용해서 코드를 작성했고 시간초과없이 통과했다.  
오늘 경영 끝나자마다 바로 자서 내일부터는 일찍 일어나 다시 수면패턴을 정상화해야겠다. 내일은 수영강습을 가는 첫 날인데 요즘 컨디션이 썩 좋지만은 않아서 잘 할 수 있을지 모르겠다.  
6시 반 기상이 목표이긴 한데 수영강습에나 늦지 않았으면 좋겠다.