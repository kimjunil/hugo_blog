---
title: "[프로그래머스] 뉴스 클러스터링"
date: 2021-12-23T12:39:07+09:00
tags:
- algorithm
- programmers
draft: false
---
> https://programmers.co.kr/learn/courses/30/lessons/17677

# 요약
두개의 문자열이 주어졌을 때 두 문자열의 자카드 유사도를 구하라!

# 제한 사항
* 각 문자열의 길이는 2 이상, 1,000 이하이다.
* 입력으로 들어온 문자열은 두 글자씩 끊어서 다중집합의 원소로 만든다. 
    * 이때 영문자로 된 글자 쌍만 유효하고, 기타 공백이나 숫자, 특수 문자가 들어있는 경우는 그 글자 쌍을 버린다. 
* 다중집합 원소 사이를 비교할 때, 대문자와 소문자의 차이는 무시한다.

# 자카드 유사도
자카드 유사도는 집합 간의 유사도를 검사하는 여러 방법 중의 하나로 알려져 있다. 두 집합 A, B 사이의 자카드 유사도 J(A, B)는 두 집합의 교집합 크기를 두 집합의 합집합 크기로 나눈 값으로 정의된다.

# Try 1
```python
import re

def solution(str1, str2):
    # 1.소문자 변환
    # 2.각 문자열을 글자쌍 배열로 분리
    # 3.특수문자가 들어있는 원소 제거
    # 4.문자쌍의 교집합/합집합 갯수 계산
    # 5.자카드유사도 계산
    
    str1, str2 = str1.lower(), str2.lower()
    list1 = [str1[i:i+2] for i in range(len(str1)-1)]
    list2 = [str2[i:i+2] for i in range(len(str2)-1)]
    
    list1 = [x for x in list1 if re.match("[a-z]{2}", x)!=None]
    list2 = [x for x in list2 if re.match("[a-z]{2}", x)!=None]
    
    A, B = list1.copy(), list2.copy()

    intersection = []
    
    for item in B:
        if item in A:
            intersection.append(item)
            A.remove(item)
        else:
            continue

    union = list1+list2
    for item in intersection:
        union.remove(item)
    
    if len(intersection)==0 and len(union)==0:
        return 65536
    else:
        return int(len(intersection)/len(union)*65536)
```

# 인상깊었던 다른사람의 풀이 1
1. isalpha() 를 사용하면 정규표현식을 사용하지 않아도 된다.
2. 다중집합의 합집합과 교집합을 구하는 과정이 간결하다.
```python
def solution(str1, str2):
    set1 = [str1[i:i+2].lower() for i in range(len(str1) - 1) if str1[i:i+2].lower().isalpha()]
    set2 = [str2[i:i+2].lower() for i in range(len(str2) - 1) if str2[i:i+2].lower().isalpha()]

    uu = sum([min(set1.count(u), set2.count(u)) for u in list(set(set1) & set(set2))])
    nn = sum([max(set1.count(n), set2.count(n)) for n in list(set(set1) | set(set2))])

    if nn == 0 and uu == 0:
        return 65536
    return int(float(uu)/float(nn) * 65536)
```


# 인상깊었던 다른사람의 풀이 2
1. lambda를 사용하였다.
```python
import math
from collections import Counter

def solution(str1, str2):
    set1 = Counter([str1[i:i+2].upper() for i in range(0, len(str1)-1) if str1[i:i+2].isalpha()])
    set2 = Counter([str2[i:i+2].upper() for i in range(0, len(str2)-1) if str2[i:i+2].isalpha()])
    J = lambda A, B: 1 if len(A) == 0 and len(B) == 0 else sum((A & B).values()) / sum((A | B).values())
    return math.floor(J(set1, set2) * 65536)
```