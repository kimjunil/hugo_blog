---
title: "[프로그래머스] LV2 전화번호 목록"
date: 2021-12-21T16:04:07+09:00
tags:
- algorithm
- programmers
draft: false
---
> https://programmers.co.kr/learn/courses/30/lessons/42577

# 요약
숫자로 이루어진 문자열 리스트가 주어졌을 때 어떤 문자열이 다른 문자열의 접두어가 될 수 있는지 Boolean으로 반환한다.

# 제한 사항
* phone_book의 길이는 1 이상 1,000,000 이하
    * 각 전화번호의 길이는 1 이상 20 이하
    * 같은 전화번호가 중복되지 않는다

# Try 1
효율성은 고려하지 않고 직관적으로 생각나는대로 만들어본 코드
```python
def solution(phone_book):
    phone_book = sorted(phone_book)
    for i, a in enumerate(phone_book):
        for b in phone_book[i+1:]:
            if b.startswith(a):
                return False
            
    return True
```
* 정확성 테스트 15/15
* 효율성 테스트 2/4

# Try 2
길이가 가장 긴 전화번호는 다른 번호의 접두어가 될 수 없으므로 무시한다
```python
def solution(phone_book):
    phone_book = sorted(phone_book)
    max_len = len(max(phone_book, key=len))
    for i, a in enumerate(phone_book):
        if len(a) >= max_len:
            continue
        for b in [x for x in phone_book[i+1:]]:
            if b.startswith(a):
                return False
            
    return True
```
* 정확성 테스트 15/15
* 효율성 테스트 3/4


# Try 3
문제의 카테고리가 해시인 것에 착안하여 접근한 풀이
```python
def solution(phone_book):
    dic = {x:idx for idx, x in enumerate(phone_book)}
    
    for i in range(len(phone_book)):
        for j in range(len(phone_book[i])):
            if dic.get(phone_book[i][:j]) != None:
                return False
            
    return True
```
* 정확성 테스트 15/15
* 효율성 테스트 4/4