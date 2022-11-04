---
layout: post
title:  "예비군과 공창컴 과제"
date:   2022-11-04 20:53:00 +0900
categories: TIL
---

# 예비군
오늘 새벽부터 군복을 입고 버스에 실려 예비군 훈련에 끌려갔다. 예상했던 것보다는 시설이나 훈련내용은 나쁘지 않았지만 사람들이 왜 예비군에 가는 것을 싫어하는지 체감할 수 있는 하루였다. 그래도 같이 끌려온 정시템 학우들과 같은 조에서 훈련받을 수 있어서 그나마 좋았다. 빨리 헌혈이나 하러가야 될 것 같다. 별로 한 것도 없는데 해가 지고 저녁이 되어버렸고 오늘 못 간 공창컴 과제를 빠르게 해치우고 쉴 예정이다.

# 공창컴 과제
## 문제1
``` python
FavSongs=['힘든 건 사랑이 아니다.', '테스형', '별 보러 가자','애국가','퍼미션 투 댄스']
FavColors=['Red','Pink','White','Blue','Ivory']
FavFoods=['사과','바나나','김치전','순두부찌개','갈비찜']
FavSongs.pop(3)
print(FavSongs)
FavColors.append('Black')
print(FavColors)
print(FavFoods[2:5])
```

## 문제2
``` python
import random
ranlist=[]
count=0
while(count<10):
  ranlist.append(random.randint(1,100))
  count+=1
print("생성된 리스트: ",end='')
print(ranlist)
print("최댓값은 %d , 최댓값의 인덱스 위치는 %d"%(max(ranlist),ranlist.index(max(ranlist))))
print("최솟값은 %d , 최솟값의 인덱스 위치는 %d"%(min(ranlist),ranlist.index(min(ranlist))))
```

## 문제5
``` python
name=['홍길동', '홍길동', '나민국']
i=0
while i<27:
  name.append('홍길동')
  i+=1
findName=input("찾고자 하는 이름을 입력하세요: ")
i=0
check=0
while i<30:
  if name[i]==findName:
    print("%s은 인덱스가 %d인 위치에 있습니다."%(findName,i))
    check=1
    break
  i+=1
if check==0:
  print('이름이 리스트에 없습니다.')

```

## 문제6
``` python
siteList=['코팡','네버','너사','다이써','야너두','옥셩','싹','이몬','삼마트','막커리']  
priceList=[1000, 2000, 3000, 1000, 3000, 2000, 1000, 2000, 1000, 1000]
cheapIndex=[]
cheapPrice=min(priceList)
i=0
while i<10:
  if priceList[i]==cheapPrice:
    cheapIndex.append(i)
  i+=1
i=0
while i<len(cheapIndex):
  j=cheapIndex[i]
  print(siteList[j],end=' ')
  i+=1
print("에서 최저가 %d원에 판매하고 있습니다."%cheapPrice)
```

공창컴 언제쯤 for 반복문 쓰게 해주시나요??  while 반복문만 써야되는 이유가 뭔지 들어나 보고 싶다.