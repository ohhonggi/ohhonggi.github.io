---
layout: post
title: Adding a Storage Layer
image:
    path: https://user-images.githubusercontent.com/33611439/224552408-9e7cc8ab-aa49-4e4e-b906-d532786045e5.png
description: >
  해당 포스트는 AWS Bootcamp에 참여하면서 Cloud Architecting 과정에서 학습한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

<style>	
	.column {
	  flex: 33.33%;
    padding: 10px;
	}
	.container {
    display: flex;
	}	

  .image {
    text-align:center;
    margin-bottom:1%;
  }
</style>

---
## Amazon S3

<div style="display:flex">
  <img width="20%" src="https://user-images.githubusercontent.com/33611439/225034487-68424958-aa8d-436c-a5da-5cacea0eea36.png">
  <ul>
    <li> Object storage service로, 방대한 양의 비정형 데이터를 저장 </li>
    <li> User가 정의한 Bucket에 data file을 object로 저장 </li>
    <li> 최대 5 TB sizedml 파일을 single object로 저장 가능 </li>
    <li> 모든 objects는 전역적으로 고유한 URL을 가짐 </li>
    <li> 모든 objects는 key, version ID, value, metadata 등을 가짐 </li>
  </ul>
</div>

### Amazon S3 benefits


<div class="container">
    <div class="column">
      <strong> Scalability </strong> <br>
      <p> • 데이터 저장 공간이 거의 무제한의 용량을 제공하여 확장성을 높임</p>
    </div>
    <div class="column">
      <strong> Security </strong>
      <p> • 저장된 데이터에 대한 접근을 제어할 수 있는 다양한 방법을 제공하여 데이터 암호화함</p>
    </div>
    <div class="column">
      <strong>Performance</strong>
      <p> • 처음 접근 시 millisecond 단위의 지연 시간과, 자주 접근하는 object에 대한 caching 지원</p>
    </div>
</div>

<div class="container">
    <div class="column">
      <strong>Durability</strong>
      <p> • 사용자가 지정한 S3 Region의 여러 데이터센터에 중복 저장하며, 손실 시 빠른 감지 및 복구를 통해 내구성을 높임 </p>
    </div>
    <div class="column">
      <strong>Availability</strong>
      <p> • 사용자가 원할 때 데이터이 신속하게 접근 가능</p>
    </div>
</div>

### Amazon S3 usecases

#### 1. Web content와 Media의 분산 저장 

<div class="image">
  <img width="80%" src="https://user-images.githubusercontent.com/33611439/225069448-7075cbfd-bcd9-4c98-b9b7-c64c3a02a2b8.png">
</div>

필요에 따라 CloudFront를 사용하여 Client에게 빠르게 데이터 전달하는 구조
{:.figcaption}

**• 저장 과정에서 Objects의 보안 방식 종류**

① 3가지의 일반적인 Bucket의 **보안 방식**

<div class="image">
  <img width="100%" src="https://user-images.githubusercontent.com/33611439/225071096-4abe0f3c-da0e-42d0-b00d-e3a1865870a0.png">
</div>

<div class="container">
    <div class="column">
      Default security 설정으로, 일반적인 User는 S3 Bucket과 Object에 접근 불가능
    </div>
    <div class="column">
      임의의 User의 Public access가 가능하도록 Security setting한 경우
    </div>
    <div class="column">
      최소 권한 원칙을 적용하여, S3 Bucket 접근이 필요한 User에게 권한 부여
    </div>
</div>
{:.figcaption}

② Amazon S3에 저장된 Objects를 **암호화**하는 2가지 방식

<div class="container">
    <div class="column">
      <strong>Server-side encryption</strong>
      <ul>
        <li> Amazon S3의 Bucket의 암호화 기능(default)사용</li>
        <li> Disk의 Object에 쓰기 전 암호화, User가 해당 Object를 Download 전 복호화</li>
      </ul>
    </div>
    <div class="column">
      <strong>Client-side encryption</strong>
      <ul>
        <li> Client가 data를 암호화한 후 S3에 upload </li>
        <li> Object마다 다른 암호화 mechanism 적용 가능 </li>
      </ul>
    </div>
</div>

#### 2. 정적 Content hosting

<div class="image">
  <img width="100%" src="https://user-images.githubusercontent.com/33611439/225085438-406eb244-5aa1-4149-9231-bf7fdc91837a.png">
</div>

Bucket의 Website hosting 설정 및 Public access 설정을 통해 Static content를 활용한 Website 구축 가능
{:.figcaption}

① Amazon S3의 Content update시 이전 내용들을 백업하는 방법 -> **Versioning**

<div class="container">
  <ul class="column">
    <li> S3에 저장하는 File을 Version별로 저장하여 Overwrites or Delete에 대한 Penalty를 protect </li>
    <li> 매번 upload 시 new version을 생성 </li>
    <li> Object의 삭제 or 이전 버전 복원 과정이 편해짐 </li>
    <li> S3 Versioning의 3가지 상태 
      <ol>
        <li> Default : Versioning 비활성화 </li>
        <li> Versioning 활성화 </li>
        <li> Versioning 중지(활성화를 적용하면 취소 불가능) </li>
      </ol>
    </li>
  </ul>

  <img class="column" 
  style="max-width:60%; height:40%; margin-top: 10%" 
  src="https://user-images.githubusercontent.com/33611439/225182622-8eca9d7b-9a27-4563-929d-362a52d2253e.png">

</div>

② Cross-Orgin Resource Sharing(CORS) 지원

<div class="image">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/225208090-4d00baef-530b-45c8-b368-65fa0c410f3b.png">
</div>

User가 생성한 CORS configuration을 적용하는 예시
{:.figcaption}

- XML document를 사용하여 CORS configuration을 적용하는 방법
<ol style="padding-left: 50px">
  <li> S3 Bucket에 접근 가능하도록 설정 </li>
  <li> Web site에 사용할 HTTP method 종류를 사용 가능하도록 설정 </li>
  <li> 다른 필요한 설정 정보 설정 </li>
</ol>


#### 3. Computation & analytics를 위한 Data store

<div class="image">
  <img width="100%" src="https://user-images.githubusercontent.com/33611439/225246706-887b91da-66d2-48e4-aa1d-bb4f6844e9fa.png">
</div>

Data 통합 및 computation을 위한 준비 패턴에 대한 예시
{:.figcaption}

- **다량의 raw data를 computation & analytics 하는 과정**
<ol style="padding-left: 50px">
  <li> 유저가 원하는 조건의 instance(EC2,EMR 등)를 생성 가능한 경우, 이를 생성하고 compute capacity를 사용할 수 있도록 가동 </li>
  <li> 처리되지 않은 raw data가 저장된 S3로부터 computation을 위한 data 추출 </li>
  <li> 데이터 통합 및 변환 알고리즘을 통해 데이터를 변환 </li>
  <li> 결과 데이터를 다른 S3 Bucket에 Load </li>
  <li> Load 후 비용 절감을 위해 compute capacity 종료 </li>
  <li> Amazon QuickSignt를 통해 처리된 데이터에서 유의미한 정보 추출 </li>
</ol>

#### 4. Back up and archive critical data

<div class="image">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/225313477-7d1f6ec3-b36a-4c64-a046-f5a456033be5.png">
</div>

On-premise data와 EC2 Data를 S3에 Backup하는 예시
{:.figcaption}

- S3가 Strongly consistent가 유지되는 이유 -> **Read after write consistency**

<div class="image">
  <img width="70%" src="https://user-images.githubusercontent.com/33611439/225318415-bdf339ff-7a7a-42b3-95e2-72e5b14a415f.png">
</div>

Object를 PUT 후, 즉시 Read 했을 때 동일한 version의 object를 가져옴
{:.figcaption}

S3 buckets의 objects에 모든 GET, LIST, PUT operation이 consistency가 지켜짐
{:.note}

---
## Storing data in Amazon S3


---
## Moving data to and from Amazom S3


---
## Choosing Regions for your architecture



