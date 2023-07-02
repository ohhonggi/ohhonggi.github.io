---
layout: post
title: Topology Sort
categories: algorithm
tags: conception
description: >
  해당 포스트는 Do-It-Algorithm Study중 위상 정렬에 대한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

## 📘 Topology Sort

- **위상** : 사물과 사물 사이에 관계 속에서 가지는 위치나 상태 -> **정점**에 적용

> **위상 정렬**이란, 각 정점들이 가지는 위상에 따라서, 그래프를 구성하는 정점들을 순서대로 정렬해서 결과값으로 출력하는 것이다.
{:.lead}

### 📜 Condition
- 위상 정렬을 할 그래프는 간선이 방향을 가지는 **유향 그래프**이어야 한다.
- 그래프 내부에 **순환**이 없어야 한다.

### 📜 Algorithm Solving Strategies
1. 진입차수가 **0**인 정점을 Queue에 삽입
<blockquote class="callout callout_info">
  <p>
  💡 <strong>진입차수</strong>는 해당 정점을 가리키는 정점의 개수를 의미함
  </p>
</blockquote>

1. Queue에서 원소를 꺼내 연결된 모든 간선을 제거
2. 간선 제거 이후에 진입차수가 0이 된 정점을 Queue에 삽입
3. Queue가 비어있을 때 까지 2~3번을 반복
   - 모든 원소를 방문하기 전에 Queue가 비는 경우 -> **Cycle** 존재
   

### 📄 Problem : <a href="https://www.acmicpc.net/problem/1516"> 백준 1516번 - 게임 개발 </a>

#### 🔎 문제 분석
- 모든 건물을 짓는데 걸리는 최단 시간 구하기
- 건물을 짓기 위해 사전에 지어저야 할 건물이 존재 -> 우선 순위가 존재하므로 **위상 정렬** 이용하여 최단 시간을 구하기

#### 💡 문제 풀이
1. 입력받은 값을 기반으로 진입 차수를 정리 및 저장
2. 진입 차수에 따라 각 건물을 짓는 데 걸리는 최단 시간 구하기 (dp를 활용하여 메모리 절약하기)
   1. 진입 차수가 0인 건물들의 경우, 건물을 짓는 데 걸리는 시간이 최단 시간임
   2. 진입 차수가 1인 건물들의 경우, 상위 건물을 짓는 데 걸리는 시간 + 해당 건물을 짓는 데 걸리는 시간 = 최단 시간
   3. 진입 차수가 2 이상인 건물들의 경우, Math.max(상위 건물을 짓는 데 걸리는 시간들) + 해당 건물을 짓는 데 걸리는 시간 = 최단 시간

