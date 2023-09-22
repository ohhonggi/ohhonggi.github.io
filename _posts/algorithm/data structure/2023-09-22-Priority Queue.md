---
layout: post
title: Priority Queue
categories: algorithm
tags: data_structure
description: >
  해당 포스트는 자료구조의 우선순위 큐에 대해서 정리한 글입니다.

sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

## 📘 Priority Queue
> **우선순위 큐**란, 데이터에 대해 우선순위가 존재하며, 그 중 **우선순위가 가장 높은 데이터**가 가장 먼저 나가는 형태의 자료구조이다.
{:.lead}

<blockquote class="callout callout_info">
  <p>
  💡 Queue에 대한 자료구조가 궁금하다면, <a href="/algorithm/2023-04-21-Stack-and-Queue/" class="flip-title">
    <span>Stack &amp; Queue</span>
  </a>
     post를 참고하시길 바랍니다.
  </p>
</blockquote>

## 📘 Heap
> 힙이란, **완전 이진트리**의 일종으로, 우선순위 큐에서 사용하는 자료구조로, 다음과 같은 특성을 가지고 있다.
{:.lead}

- 여러 데이터 중, 최대값이나 최솟값을 빠르게 찾아내기 위한 자료구조
- 일종의 반 정렬 상태(느슨한 정렬 상태)를 유지
  - 부모 노드가 자식 노드보다 우선순위가 항상 높다
  - 부모와 자식 관계는 항상 '**부모값 ≧ 자식값**'
- 이진 탐색 트리와 달리, **중복**을 허용

### 📚 종류
- **Max Heap (최대 힙)**
  - 부모 노드의 키가 자식 노드의 키보다 큰 경우
- **Min Heap (최소 힙)**
  - 부모 노드의 키가 자식 노드의 키보다 작은 경우

<img class="centered" width="90%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/f2a26e29-3622-4d83-b63c-8570a245de6e">

Min Heap과 Max Heap (출처 - <a href="https://www.geeksforgeeks.org/heap-data-structure/#:~:text=complete%20binary%20tree.-,Heap%20Data%20Structure,-Operations%20of%20Heap">geeksforgeeks</a>)
{:.figcaption}

### 📁 저장 구조
힙은 **배열**을 사용하여 데이터를 저장한다.

- **Parent** Index : a[(i-1)/2]
- **Left Child** Index : a[i*2 + 1]
- **Right Child** Index : a[i*2 + 2]

<img class="centered" width="90%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/4ac1bf11-d39c-4f51-959b-192657b5e270">

Max Heap이 배열에 저장된 모습
{:.figcaption}

### 📜 힙 정렬 과정
힙 정렬은 '가장 우선순위가 큰 값이 루트에 위치'하는 특성을 이용하는 정렬 알고리즘으로, 먼저 힙의 삭제 과정에 대해서 알아야 합니다.

#### 💡 힙의 삭제 과정
1. 힙의 루트를 삭제
2. 힙의 맨 마지막 원소를 루트로 이동
3. 루트에 대하여 다음과 같은 작업을 반복
  1. 자식 중, 자신보다 우선순위가 큰 자식과 자리 이동
  2. 자식이 자신보다 우선순위가 작거나, 리프 노드에 다다르는 경우 종료 

<img class="centered" width="90%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/43ab0910-c0b8-4fb0-9ae0-5a5a6a9ecf40">

<img class="centered" width="90%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/a2b034e6-03e4-4699-97d7-728dd9b6c9c5">

<img class="centered" width="95%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/f39ef8bf-fa99-47ed-aa5e-b5ac246a0918">

<img class="centered" width="95%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/2c592f49-bc44-432a-87f2-99b637e2e8d6">

<blockquote class="callout callout_info">
  <p>
    ✅ <strong >힙의 삽입</strong>의 경우, 힙의 마지막에 이은 다음 위치에 삽입되는 것 이외에는 위 3번과 같이 힙의 성질을 만족하는 과정으로 진행된다.
  </p>
</blockquote>

#### 💡 힙의 정렬 과정
삭제 과정을 기반으로 한 힙의 정렬 과정은 다음과 같습니다.
1. 변수 i값을 n-1로 초기화
2. a[0]과 a[i]를 Swap
3. a[0],a[1],･･･,a[i-1]을 힙이 되도록 정렬 (힙 삭제의 3번 과정과 동일)
4. i값을 감소시키며 0이 될 때 까지 2로 돌아가 반복

<img class="centered" width="90%" src="https://github.com/ohhonggi/Today_my_learning/assets/33611439/43ab0910-c0b8-4fb0-9ae0-5a5a6a9ecf40">

Heap의 정렬 과정
{:.figcaption}

### ⏰ 시간복잡도
<p>힙 정렬은 선택 정렬을 응용한 알고리즘입니다. 단순 선택 정렬과 달리, 루트를 꺼내는 것으로 선택의 시간복잡도는 <strong>O(1)</strong>에 해당하지만, 힙 정렬 과정에서 '다시 힙으로 만드는' 작업을 수행하므로 시간복잡도는 <strong style="color:red">O(logn)</strong>에 해당합니다.</p>

> 결국 '다시 힙으로 만드는' 작업을 **반복**하기 때문에, 전체 정렬에 필요한 시간복잡도는 <strong style="color:red">O(nlogn)</strong>임을 알 수 있습니다.
{:.lead}

### 📄 Problem : <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42626"> 더 맵게 </a>

#### 🔎 문제 분석
- 모든 음식에는 스코빌 지수(맵기 정도)가 존재하며, 이를 주어진 K 수 이상으로 만드는 것 : **최종 조건**
- 스코빌 지수 K보다 작은 음식 중 **스코빌 지수가 가장 낮은 두 음식**을 찾아 새로운 음식을 만들어 최종 조건을 만족시키기
  -  섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
- 모든 음식의 스코빌 지수를 K이상으로 만들기 위해 섞어야 하는 최소 횟수 구하기(불가능할 경우 **-1**) : 결과값

#### 💡 문제 풀이
1. 모든 음식 정보를 우선순위 큐(최소 힙)을 사용하여 정렬
2. queue의 루트(최소 스코빌 지수값)가 k보다 작거나, queue의 원소 개수가 2개 이상일 때 3~5 반복
3. queue에서 원소(스코빌 지수값) 2개 삭제
4. 두 원소를 섞어 새로운 음식 생성
5. queue에 삽입 후, 2번으로 돌아가 반복
6. queue의 루트가 K보다 같거나 큰 경우 섞은 횟수를, 아닌 경우 -1 반환


~~~java
import java.util.PriorityQueue;
import java.util.Arrays;
import java.util.stream.Collectors;

class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        PriorityQueue<Integer> queue = new PriorityQueue(
            Arrays.stream(scoville).boxed().collect(Collectors.toList()));
        
        while (queue.peek() < K && queue.size() > 1){
            queue.add(queue.remove() + (queue.remove()*2));
            answer++;
        }
        
        return queue.peek() < K ? -1 : answer;
    }
}
~~~