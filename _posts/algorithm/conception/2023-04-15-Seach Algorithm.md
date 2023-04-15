---
layout: post
title: Search Algorithm
categories: algorithm
tags: conception
description: >
  해당 포스트는 Do-It-자료구조-Algorithm 책 내용 중 검색 알고리즘에 대해 공부한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

> 데이터 집합에서 원하는 값을 가진 요소를 찾아내는 알고리즘
{:.lead}

- 검색은 특정 <span style="color: blue">항목(Key)</span>에 대한 <span style="color: red">데이터(Value)</span>를 찾아내는 것이다.
- 검색은 데이터를 저장하는 방식인 자료구조에 많은 영향을 받는다.
  
### 📜 Array Search Algorithm 종류
1. **Linear Search**: 정렬되지 않은 데이터 모임에서 검색 수행
2. **Binary Search**: 정렬된 데이터 모임에서 빠른 검색 수행
3. **Hasing**: 추가, 삭제가 자주 일어나는 데이터 모임에서 아주 빠른 검색 수행
   - Chaining : 같은 해시값의 데이터를 선형 리스트로 연결하는 방법
   - Open addressing : 데이터를 위한 해시값이 충돌할 때 재해시하는 방법

<blockquote class="callout callout_info">
  <p>
  💡 <strong>Consideration</strong> : 검색만 하는 경우에는 빠른 알고리즘을 선택하지만, <strong>데이터 추가 & 삭제</strong> 작업의 반복은 여러 비용을 종합적으로 평가하여 알고리즘을 선택해야 한다.
  </p>
</blockquote>


#### 🔎 Linear Search (= Sequential Search)
원하는 키값을 갖는 요소를 만날 때 까지 **맨 앞에서부터 순서대로 요소를 검색**하는 알고리즘으로, <strong style="color:red">O(n)</strong>의 시간복잡도를 가진다.

<img class="centered" width="60%" src="https://user-images.githubusercontent.com/33611439/232203192-f467a44c-73df-4a6e-91ab-d67496ef43b2.png">

Key(2)를 찾기 위한 선형 검색 과정
{:.figcaption}

- **Terminate Condition**
  1. 종료 검색할 값과 같은 요소를 발견한 경우             ➡️ 검색 **성공**
  2. 종료 검색할 값을 발견하지 못하고 배열의 끝을 지나간 경우 ➡️ 검색 **실패**

#### 🔎 Binary Search
데이터가 **키값으로 정렬**되어있다는 조건 하에, 선형 검색보다 빠르게 탐색이 가능한 알고리즘으로, <strong style="color:red">O(log n)</strong>의 시간복잡도를 가진다.

- **Binary Search Process**

<ol style="margin-left: 15px"> 
  <li class="margin"> 검색 범위의 맨 앞 인덱스를 pl, 맨 끝 인덱스를 pr, 중앙 인덱스를 pc라고 가정할 때, 최초 검색 시작 시 pl은 0, pr은 n-1, pc는 (n-1)/2로 정하여 탐색을 시작한다.
  </li>

  <img class="centered" width="60%" style="margin-down: 20px" src="https://user-images.githubusercontent.com/33611439/232205532-9f63bf88-4238-4f7f-b8a9-a2fc18a39cdc.png">

  <li class="margin"> 찾으려는 key의 값을 pc와 비교하여 탐색 범위를 좁힌다. (약 절반으로 줄어듦)

  <img class="centered" width="60%" src="https://user-images.githubusercontent.com/33611439/232205675-d7839767-aeea-4cfd-9570-3e02a90dcf41.png">
    <ul class="margin">
      <li> a[pc] > key 일 때: 범위를 a[pc+1] ~ a[pr]로 범위를 수정</li>
      <li> a[pc] < key 일 때: 범위를 a[pl] ~ a[pc-1]로 범위를 수정 </li>
    </ul>
  </li>

  <li  style="margin-top: 15px"> 종료 조건에 다다를때 까지 1~2번을 반복한다.  
  </li>

  <img class="centered" width="60%" src="https://user-images.githubusercontent.com/33611439/232206043-dd0e3ffb-eb9c-463d-ab60-6b89775cc3b0.png">
</ol>

key(39)를 찾은 경우
{:.figcaption}

- **Terminate Condition**
  1. : a[pc]가 key와 일치하는 경우 ➡️ 검색 **성공**
  2. : 검색 범위가 더 이상 없는 경우 ➡️ 검색 **실패**

#### Arrays.binarySearch 함수 분석
Java의 표준 라이브러리 중, binary search를 제공하는 배열의 메서드

~~~<java>
static int binarySearch(T [] array, T key)
~~~

- **Parameters**
  - 첫 번째 파라미터에는 오름차순으로 정렬된 배열을 입력받는다.
  - 두 번째 파라미터에는 찾아야 할 요소인 key를 입력받는다. 

- **검색 결과**
<ol>
  <li> 검색에 <strong>성공</strong>한 경우, key와 일치하는 요소의 <strong>인덱스</strong>를 반환한다. </li>
  <blockquote class="callout callout_warning">
    <p>
    🚧 <strong>Consideration</strong> : key와 일치하는 요소가 여러 개일 경우, 맨 앞에 있는 인덱스가 아니라, <strong>무작위로 인덱스를</strong> 반환한다.
    </p>
  </blockquote>

  <li class="margin"> 검색에 <strong>실패</strong>한 경우, '배열 안에 key가 있어야 할 위치(삽입 포인트)를 추정할 수 있는 값'을 반환한다.
    <ul>
      <li>삽입 포인트가 x라 할 때, 반환값은 <strong>-x-1</strong>로, 검색하기 위해 지정한 key보다 큰 요소 중 첫 번째 요소의 인덱스를 의미함</li>
      <li>모든 요소가 key보다 작다면 <strong>배열의 길이</strong>를 삽입 포인트로 반환함</li>
    </ul>
    
   </li>

</ol>

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/232238931-d276f161-8f9b-4917-9dac-bf8c48ca6700.png">

31 큰 요소 중 첫 번째 요소의 인덱스인 -(5+1)를 반환하는 예시
{:.figcaption}


#### 🔎 Hasing
검색뿐 아니라 데이터의 추가 및 삭제를 효율적으로 수행하는 방법으로, 데이터를 저장할 **위치(Hash value)**를 **연산(Hash function)**으로 구하여 검색, 추가, 삭제를 효율적으로 수행

- **Hash function** : 데이터를 저장할 위치(index)를 구하는 연산을 위한 함수로, key값에 대해 <span style="color: red">중복이 적은 함수</span>를 지향
- **Hash value** : 데이터가 Hash function에 의해 계산된 값
- **Hash table** : Hash value를 인덱스로 하여 기존의 데이터를 저장한 배열

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/232209123-89952625-1732-4af3-8c31-ecc34c5aa557.png">

배열 삽입 과정의 단점 (요소 이동에 필요한 복잡도가 **O(n)**에 해당)
{:.figcaption}

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/232210714-cf71cf5a-5c15-48b1-b490-785315d13401.png">

Hasing의 삽입 과정
{:.figcaption}


### ⚙️ Complexity
알고리즘의 성능을 객관적으로 평가하는 기준

- **Time complexity(시간 복잡도)**: 실행에 필요한 시간을 평가한 것
- **Space complexity(공간 복잡도)**: 기억 영역과 파일 공간이 얼마나 필요한가를 평가한 것

<div class="container">
  <table class="column">
    <th> Algorithm </th>
    <th> Time complexity </th>
    <tr>
      <td>Linear search</td>
      <td>O(n)</td>
    </tr>
    <tr>
      <td>Binary search</td>
      <td>O(log n)</td>
    </tr>
    <tr>
      <td>Hasing</td>
      <td>O(1)</td>
    </tr>
  </table>
  <img width="55%" src="https://user-images.githubusercontent.com/33611439/232207218-892c50a7-78a0-4735-b713-bbef77afa05b.png" style="object-fit: contain">
</div>


복잡도와 증가율 (n : 반복 실행 횟수)
{:.figcaption}

<blockquote class="callout callout_info">
  <p>
  📘 <strong>알고리즘의 전체 복잡도</strong> : 2개 이상의 복잡도로 구성된 알고리즘의 전체 복잡도는 <strong>차수가 더 높은 쪽</strong>의 복잡도가 지배함.
  </p>
</blockquote>


### 📑 Reference
- Do it! 자료구조와 함께 배우는 알고리즘 입문 - 자바 편: 전면개정판. (2022). (pp.94-129, 393-394): 이지스퍼블리싱 ㈜.