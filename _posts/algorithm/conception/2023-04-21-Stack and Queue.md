---
layout: post
title: Stack & Queue
categories: algorithm
tags: conception
description: >
  해당 포스트는 Do-It-자료구조-Algorithm 책 내용 중 Stack과 Queue에 대해 공부한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

## 📘 Stack

> 데이터를 일시적으로 쌓아 놓는 자료구조로, 가장 나중에 넣은 데이터를 가장 먼저 꺼내는 후입선출(= LIFO, Last In First Out)이다.
{:.lead}

- 데이터를 넣는 작업을 **푸시(push)**, 데이터를 꺼내는 작업을 **팝(pop)**이라 한다.
- 데이터의 출입이 이루어지는 곳을 **꼭대기(top)**, 스택에 가장 아래부분을 **바닥(bottom)**이라 한다.

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/233575354-ccf29f1c-a4b5-49d0-a09f-7512d2b58452.png">

Stack의 push와 pop
{:.figcaption}

## 📘 Queue

> 스택과 같이 데이터를 일시적으로 쌓아 놓는 자료구조이나, 가장 먼저 넣은 데이터를 가장 먼저 꺼내는 선입선출(= FIFO, First In First Out)이다.
{:.lead}

- 데이터를 넣는 작업을 **삽입(add)**, 데이터를 꺼내는 작업을 **삭제(remove)**이라 한다.
- 데이터가 나오는 쪽을 **프런트(front)**, 데이터를 넣는 쪽을 **리어(rear)**이라 한다.

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/233600231-01c5f250-3dd4-4ede-afaf-5215e57d915c.png">

Queue의 add와 remove
{:.figcaption}

### 📖 변수와 메서드

#### 변수의 종류
변수는 데이터를 담는 배열 **stk**, 자료구조의 용량을 뜻하는 **capacity**, 새로운 데이터를 삽입할 포인터 **ptr**로 이루어진다 

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/233581943-f65c98e9-3393-4b6a-b2a7-1da56b2d412c.png">

스택 구현 예시
{:.figcaption}

<blockquote class="callout callout_info">
  <p>
  💡 여기서 '포인터' ptr 은 포인터변수를 의미하지 않는다. 새로운 데이터를 삽입할 인덱스를 저장하는 변수이며,'배열의 인덱스를 가리킨다'는 의미로 '포인터'라고 함.
  </p>
</blockquote>

#### 메서드 종류
- **push()** : 정수 데이터를 넣는 메서드로, 스택이 가득 찰 경우에는 예외로 OverflowIntStackException를 발생
- **pop()** : top(front)에 있는 데이터를 삭제하는 메서드로, 스택이 비어있는 경우에는 예외로 EmptyIntStackException를 발생
- **peek()** : top(front)에 있는 데이터를 EmptyIntStackException를 발생
- **clear()** : 배열에 쌓여 있는 모든 데이터를 삭제하는 메서드
- **indexOf(int x)** : 배열 stk에 x와 같은 값의 데이터를 찾아 인덱스를 반환하는 메서드로, 실패할 경우 -1을 반환
- **capacity()** : 배열의 용량을 반환
- **size()** : 배열에 쌓여 있는 데이터 개수(ptr값) 반환
- **isEmpty()** : 배열이 비어있는지 여부를 boolean값으로 반환
- **isFull()** : 배열이 가득찼는지 검사하는 메서드


### 📘 Ring Buffer
배열의 맨 뒤가 맨 앞과 연결되었다고 보는 자료구조이다. 앞 자료구조의 변수 중 포인터에서 차이를 보이며, front와 rear가 논리적으로 의미가 다르다.

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/233657033-d6691d0d-1713-416c-b4da-2284a4c1ff0f.png">

Ring Buffer를 사용한 queue 구현 예시
{:.figcaption}


- 논리적으로 맨 앞 요소의 인덱스를 의미하는 **front** 변수를 가진다.
- 논리적인 맨 뒤 요소의 이전 인덱스를 의미하는 **rear** 변수를 가진다. (다음 요소를 add하기 위한 인덱스)
- 추가적으로, 현재 데이터의 개수를 의미하는 **num** 변수를 가진다. (front와 rear의 포인터 값이 같은 경우 자료구조에 담긴 데이터의 양을 알 수 없기 때문)


#### Ring Buffer를 사용한 queue의 데이터 이동과정

<img class="centered" width="80%" src="https://user-images.githubusercontent.com/33611439/233665140-a4063d28-ba3b-4b56-ac72-0f5e72c9592f.png">

Ring Buffer의 add와 remove 예시
{:.figcaption}

<blockquote class="callout callout_info">
  <p>
  💡 Ring Buffer는 '오래된 데이터를 버리는' 용도로 사용 가능하다. 제한된 크기 n의 배열에 대해 지속적인 데이터가 입력될 때, 가장 최근에 들어온 데이터 n개만 저장되고 나머지는 버려지게 된다.
  </p>
</blockquote>



### 📑 Reference
- Do it! 자료구조와 함께 배우는 알고리즘 입문 - 자바 편: 전면개정판. (2022). (pp.130-161): 이지스퍼블리싱 ㈜.