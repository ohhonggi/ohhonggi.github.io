---
layout: post
title: Dynamic Programming Algorithm
categories: algorithm
tags: conception
description: >
  해당 포스트는 삼성 S/W 역량 알고리즘 특강 과정 중, DP에 대한 내용을 정리한 글입니다.

sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

## 📘 Memoization
> 메모이제이션이란, 함수 실행 과정 중, 이전에 계산한 값을 **메모리에 저장**함으로써 같은 계산 과정을 생략하는 최적화 기술로, DP의 핵심 기술이다.
{:.lead}

## 📘 Dynamic Programming
> 동적 계획 알고리즘은 그리디 알고리즘과 같이 **최적화 문제**를 해결하는 알고리즘으로, 큰 크기의 문제를 부분 문제들로 쪼개어 해결함으로써 원래 주어진 큰 크기의 문제를 해결하는 상향식 방법으로 접근한다.
{:.lead}

<blockquote class="callout callout_info">
  <p>
  💡 DP는 일반적으로 상향식 방법으로 접근하지만, 하향식 방법으로도 접근이 가능하다.
  </p>
</blockquote>

### 📜 Condition
- **최적** 부분문제 구조 (Optimal substructure)
  - 문제가 최적화의 원칙을 만족해야 함
  - 어떤 문제의 해가 최적일 떄, 그 해를 구성하는 작은 문제들의 해 역시 최적이어야 한다는 것이 최적화의 원칙
- **중복** 부분문제 구조 (Overlapping subproblems)
  - 문제의 부분 문제들이 순환적인 성질이 존재하며, 이는 이전에 계산되어졌던 작은 문제의 해가 중복적으로 필요하게 되는 경우가 발생하고, 이를 재활용하기 위해 메모리에 저장함
  - 이후 저장된 부분문제의 해들이 다시 필요할 때(=순환적인 성질) 메모리에 저장된 값을 재활용함으로써 중복 계산을 피할 수 있는 방식


### 📜 Algorithm Solving Strategies
1. 최적해 구조의 특성 파악
   - 문제를 부분 문제로 분할
2. 최적해의 값을 재귀적으로 정의
   - 부분 문제의 최적해 값에 기반하여 문제의 최적해 값을 정의
3. 상향식 방법으로 최적해 값 계산
   - 가장 작은 부분 문제의 해를 구하여 메모리에 저장
   - 부분 문제의 해를 이용하여 상위 부분 문제의 최적해를 구함
   

### 📄 Problem1 : 이항계수 구하기

#### 🔎 문제 분석
- 이항 다항식 x + y의 거듭제곱 (x+y)ⁿ에 대해서, 전개한 각 항 xᵏyᴺ⁻ᵏ의 **계수 값**을 구하는 정리
- xᵏyᴺ⁻ᵏ의 계수는 n개에서 k개를 고르는 조합의 가짓수인 nCk를 구함을 의미 

#### 💡 문제 풀이
1. 파스칼의 삼각형을 이용한 공식 적용 <br> <br>
$$
\begin{aligned}
  _nC_k = \frac{n!}{k!(n-k)!}
\end{aligned}
$$

1. 기존 공식에 DP 활용 <br> <br>
$$
_nC_k =
\left(\begin{array}{ccc}
\left(\begin{array}{ccc}
 _n-_1C_k-_1 +  _n-_1C_k
\end{array}\right) & if & (1 < k < n) \\
1                  & if & (k = 0 \left |  \right | k = n)
\end{array}\right)
$$

### 📄 Problem2 : LIS(Longest Increasing Subsequence)

#### 🔎 문제 분석
- 수열이 주어졌을 때, 주어진 수열의 순서를 유지하면서 크기가 점진적으로 커지는 **가장 긴 부분수열**을 추출하는 문제

#### 💡 문제 풀이
1. Brute-force 접근 방법
   - 수열의 모든 부분 집합을 구하고, 그 부분 집합 중 증가 수열인 집합을 판별하고, 이를 통해 가장 긴 값을 구함
   - 시간복잡도 : <strong style="color:red"> O(2ⁿ) </strong>

2. DP 접근 방법 
   - LIS[i] = a₁, a₂, ..., aᵢ까지의 숫자열 중, 최장 부분 수열 길이
     - LIS[i]가 aᵢ를 포함하지 않는 경우, LIS[i] = LIS[i-1]
     - LIS[i]가 aᵢ를 포함하는 경우 LIS[i] = max(LIS(1)..LIS(i-1)) + 1
   - 시간복잡도 : <strong style="color:red"> O(n²) </strong>

3. DP와 이진 검색을 활용한 방법
   - C[k] : 길이 k의 증가 수열에 대하여 가장 작은 값을 C[k]에 저장
   - 각 위치에서 C[]를 갱신하기 위해 이진 검색 수행
   - 시간복잡도 : <strong style="color:red"> O(nlogn) </strong>

### 📄 Problem3 : 모든 쌍 최단 경로

#### 🔎 문제 분석
- 그래프에 대한 정보가 주어졌을 때, 각 정점 사이의 최단 경로는 얼마인지 구하는 문제

#### 💡 문제 풀이 
1. Brute-force 접근 방법
   - 한 정점에서 다른 정점까지의 모든 경로의 길이를 구하고, 그 중 최소 찾기
   - 그래프가 n개 정점을 가지고, 완전그래프라 가정했을 때, 정점 i에서 정점 j로 가는 경로의 수를 계산
   - 시간복잡도 : <strong style="color:red"> O((n-2)!) </strong>
     - i에서 출발하여 처음 도착 가능한 정점의 가지 수는 n-2, 그 중 하나를 선택한 후 도착 가능한 정점의 가지 수는 n-3, 이 과정을 통해 시간복잡도는 O((n-2)!)임을 알 수 있음

2. DP 접근 방법
   1. 각 점을 시작점으로 정하여 다익스트라의 최단 경로 알고리즘을 수행 
      - 시간복잡도는 배열 사용 시 (n-1)xO(n²) = <strong style="color:red"> O(n³) </strong>
   2. 모든 쌍의 경로 존재 여부를 찾아내는 플로이드-워샬 알고리즘 수행
      - 시간복잡도는 1번과 동일, 하지만 코드가 간결
      - Dijᵏ = 점 {1, 2 ,...,k}만을 경유 가능한 점들로 고려하여 점 i로부터 점 j까지의 모든 경로 중 가장 짧은 경로의 거리
      ~~~java
      // D[i][j] = 선분 (i, j)의 가중치
        for (int k = 0; k < n; k++){
          for (int i = 0; i < n; i++){
            for (int j = 0; j < n; j++){
              if (i == j)
                continue;
              if (D[i][j] > D[i][k] + D[k][j]){
                D[i][j] = D[i][k] + D[k][j];
              }
            }
          }
        }
      ~~~


### 📄 Problem4 : 최소 여행 경비 문제 - TSP(Traveling Salesman Problem)

#### 🔎 문제 분석
- 시작 정점에서 최소 경비로 모든 정점을 방문하여 시작점으로 돌아오는 방법

#### 💡 문제 풀이
1. Brute-force 접근 방법
   - 모든 일주 여행 경로를 고려한 후, 가장 짧은 일주 여행 경로 선택 -> 가능한 일주 경로의 개수는 (n-1)!
   - 시간복잡도 : <strong style="color:red"> O((n-1)!) </strong>

2. DP 기반 접근
   - V는 모든 정점의 집합, A는 V의 부분집합이라 가정
   - D[Vi][A] = A에 속한 각 정점을 한 번씩만 거쳐서 vi에서 v1으로 가는 최단 경로의 길이
   - 시간복잡도 : <strong style="color:red"> O(n²2ⁿ) </strong>

$$
\begin{aligned}
  D[\nu_i][V-\left \{ \nu_i \right \}] 
  = min_{2\leq j\leq n}(W[1][j]+D[\nu_j][V- \left \{ \nu_i,\nu_j \right \} ])
\end{aligned}
$$

V₁에서 Vj로의 거리와 Vj를 제외한 거리 합
{:.figcaption}

  - 일반적으로 표현하면 i ≠ 1 이고, Vᵢ가 V에 속하지 않을 때, 다음과 같이 나타냄

$$
\left \{
\begin{array}{c}
D[\nu_i][V] \begin{array}{ccc}
= min_{\nu_i\in V}(W[i][j]+D[\nu_j][V- \left \{\nu_j \right \}]) & if & V\neq \varnothing 
\end{array} \\

D[\nu_i][\varnothing] = W[i][1]
\end{array}
\right \}
$$

~~~java
// bitmask를 활용한 TSP구현 (O(N²2ⁿ))
public int dp(int index, int visited){
  if (v[index][visited] != -1)
    return v[index][visited];
  
  v[index][visited] = Integer.MAX_VALUE;

  if (visited == ((1 << n)-1))
    return v[index][visited] = weight[index][visited];
  
  for (int i = 1; i<n; i++){
    if ((visited & (1 << i)) == 0){
      int nextV = visted | (1 << i);
      v[index][visited] = Math.min(v[index][visited], dp(i ,nextV));
    }
  }
  return v[index][visited];
}
~~~

