---
layout: post
title: Greedy Algorithm
categories: algorithm
tags: conception
description: >
  해당 포스트는 Algorithm 중 그리디 알고리즘에 대해 공부한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

> 선택의 순간마다 가장 최적의 방법을 찾아 최종적인 해답에 도달하는 알고리즘
{:.lead}

- 결국 최적의 해를 구하는 방법을 사용할 때 가장 적합한 방법이다
- 문제를 풀기 위한 최소한의 아이디어를 떠올리는 것이 관건 (단, 아이디어의 **정당성 분석**이 중요!)
- 순간마다의 선택은 그 **순간에(지역적)** 대해 최적의 선택일 수 있지만, 이 과정을 통해 도달한 **최종적인(전역적)** 해가 최적이라는 보장이 없다


<blockquote class="callout callout_info">
  <p>
  💡 <strong>정당성 분석</strong> : 지역적으로 최적이면서, 전역적으로 최적인 해를 구하는 방법인지 분석하는 것 
  </p>
</blockquote>

### 🔑 Greedy Algorithm 해결 방법
1. **선택 절차** : 현재 상태에서 최적의 해답을 선택
2. **적절성 검사** : 선택된 해가 문제의 조건을 만족하는지 검사
3. **해답 검사** : 원래의 문제가 해결되었는지 검사하고, 해결되지 않았을 경우 1번으로 돌아가 반복

- ####  문제의 정당성 파악
탐욕 알고리즘이 작동하기 위해서는 **탐욕적 선택 조건**과 **최적 부분 구조 조건**의 두 선택 조건이 만족되어야 한다.

  1. **탐욕적 선택 속성** : 현재 선택이 이후의 선택에 영향을 주지 않는다는 조건
  2. **최적 부분 구조** : 문제에 대한 최종적인 해결 방안은 부분 문제에 대한 최종적인 해결 방안으로 이루어진다는 조건

### 📄 Greedy Algorithm 문제 : <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42862?language=java"> 프로그래머스 체육복 문제 </a>

- **해결 방법 적용**
  1. 선택 절차 : 체육이 가능한 학생 수를 늘리기 위해 앞 or 뒤 학생을 선택
  2. 적절성 검사
     1. 선택한 학생이 여유분의 체육복을 가지고 있는지 검사
     2. 선택한 학생이 체육복을 도난당했는지 검사
  3. 해답 검사 : 도난 당한 학생 수가 남아있는지 검사하고, 남아있으면 1번 반복

- **유의사항**
  1. 여벌 체육복을 가져온 학생은 체육복을 도난당할 수 있음
  2. 도난당한 학생 정보가 담긴 배열(lost)과, 여벌의 체육복을 가져온 학생들의 정보가 담긴 배열(reserve)은 체격순으로 정렬되어 있지 않음

### Reference
<a href="https://www.youtube.com/watch?v=2zjoKjt97vQ"> 이코테 2021 강의 몰아보기 - 2. 그리디 & 구현 </a> <br>
<a href="https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%83%90%EC%9A%95%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-greedy-algorithm/"> HANAMON - [알고리즘] 탐욕 알고리즘(Greedy Algorithm) </a>