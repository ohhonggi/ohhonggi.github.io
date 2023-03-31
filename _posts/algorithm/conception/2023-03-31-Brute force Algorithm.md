---
layout: post
title: Brute force Algorithm
categories: algorithm
tags: conception
description: >
  해당 포스트는 Algorithm 중 완전탐색 알고리즘에 대해 공부한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

> Brute(무식한) + Force(힘), 즉 가능한 모든 경우의 수를 탐색하여 해답을 찾는 방법
{:.lead}

- **완전 탐색 알고리즘**이라고도 부르며, 효율성에 상관 없이 확실한 해답을 찾으려 할 때 유용하다.
- 완전 탐색 시간복잡도를 분석하였을 때, <span style="color:red">문제의 **제한시간**에 벗어나지 않는지 판단하는 것</span>이 중요하다.

### 🔑 Brute Force Algorithm 종류
- **선형 구조** : 자료를 구성하는 원소들을 하나씩 순차적으로 나열된 구조
  - <span style="color:blue">순차 탐색</span> : 해답의 범위에서 처음부터 끝까지 탐색하는 방법
    - 시간복잡도 : O(n)
    - 풀이 방법
      1. 주어진 문제를 선형 구조로 구조화
      2. 구조화된 문제 공간을 적절한 방법으로 모든 해답을 구할 때 까지 탐색
      3. 탐색한 해답을 문제의 정답에 맞게 정리
- **비선형 구조** : 자료를 구성하는 각 원소 뒤에 여러 개의 원소가 존재 가능한 구조
  - <span style="color:blue">DFS</span> : Depth First Search, 깊이를 우선으로 탐색하는 방법
  - <span style="color:blue">BFS</span> : Breadth First Search, 너비를 우선으로 탐색하는 방법

DFS와 BFS는 추후 따로 다룰 예정입니다.
{:.note}

### 📄 Brute Force Algorithm 문제 : <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42862?language=java"> 백준 ~ 문제 </a>



### Reference
<a href="https://velog.io/@mygomi/TIL-34-%EB%B8%8C%EB%A3%A8%ED%8A%B8-%ED%8F%AC%EC%8A%A4Brute-Force"> TIL 34 | 알고리즘 기법 - 브루트 포스(Brute Force) </a> <br>
