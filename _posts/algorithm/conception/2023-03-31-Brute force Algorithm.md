---
layout: post
title: Brute force Algorithm
categories: algorithm
tags: conception, Brute force
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
  - **순차 탐색** : 해답의 범위에서 처음부터 끝까지 탐색하는 방법
    - 시간복잡도 : O(n)
    - 풀이 방법
      1. 주어진 문제를 선형 구조로 구조화 (구조화)
      2. 구조화된 문제 공간을 적절한 방법으로 모든 해답을 구할 때 까지 탐색 (탐색)
      3. 탐색한 해답을 문제의 정답에 맞게 정리 (정리)
- **비선형 구조** : 자료를 구성하는 각 원소 뒤에 여러 개의 원소가 존재 가능한 구조
  - **DFS** : Depth First Search, 깊이를 우선으로 탐색하는 방법
  - **BFS** : Breadth First Search, 너비를 우선으로 탐색하는 방법

DFS와 BFS는 추후 따로 다룰 예정입니다.
{:.note}

### 📄 Brute Force Algorithm 문제 : <a href="https://www.acmicpc.net/problem/1969"> 백준 1969번 - DNA </a>

- **문제 분석** 
  - 유의사항
    - Hamming Distance의 합이 동일한 DNA가 여러 개 있을 때에는 **사전순**으로 가장 앞서는 것을 출력
  - 시간복잡도 분석 : 유전자 분석 물질 종류 * 최대 DNA 수 * 최대 DNA 길이 -> **순차 탐색** 적용 가능
<div>
$$ 
      \begin{aligned}
      4 * 1000 * 50 = 10^5 * 2  < 10^9 * 2 &
      \end{aligned}
$$
</div>
약 2초의 시간복잡도 시간 기준
{:.figcaption}

- **풀이 방법**
  1. DNA의 n번째 자리수 알파벳과 DNA의 물질에 해당하는 알파벳이 다른지 비교하여 Hamming Distance의 합 구하기
  2. n번째 자리수의 Hamming Distance의 합이 가장 적은 DNA 물질 찾기
  3. DNA의 끝 자리수에 도달할 때 까지 반복

- **작성 코드**
~~~<java>
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    StringTokenizer st = new StringTokenizer(br.readLine());
    int n = Integer.parseInt(st.nextToken());
    int m = Integer.parseInt(st.nextToken());
    String[] dna = new String[n];
    char[] material = {'A', 'C', 'G', 'T'};
    int distance = 0,
        minCount, curCount;
    char curChar = 0;

    String result="";

    for (int i = 0; i < n; i++) {
        dna[i] = br.readLine();
    }

    for (int i = 0; i < m; i++) {
        minCount = Integer.MAX_VALUE;
        for (int j = 0; j < material.length; j++) {
            curCount = 0;
            for (int k = 0; k < n; k++) {
                if (material[j] != dna[k].charAt(i)){
                    curCount++;
                }
            }
            if (minCount > curCount){
                minCount = curCount;
                curChar = material[j];
            }
        }
        distance += minCount;
        result += curChar;
    }
    System.out.println(result + "\n" + distance);
}
~~~

### Reference
<a href="https://velog.io/@mygomi/TIL-34-%EB%B8%8C%EB%A3%A8%ED%8A%B8-%ED%8F%AC%EC%8A%A4Brute-Force"> TIL 34 | 알고리즘 기법 - 브루트 포스(Brute Force) </a>
