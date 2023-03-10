---
layout: post
title: Introducing Cloud Architecting
image:
    path: https://user-images.githubusercontent.com/33611439/223368623-20187405-9d44-4ef9-af1e-45b928f8d460.png
description: >
  해당 포스트는 AWS Bootcamp에 참여하면서 Cloud Architecting 과정에서 학습한 내용을 정리한 글입니다.
sitemap: false
hide_last_modified: true
---

- Table of Contents
{:toc .large-only}

## The AWS Well-Architected Framework

> **Cloud Architecture** : Cloud Service와 기능을 사용하여 조직의 기술적 요구와 비즈니스 사용 사례를 충족하는 솔루션에 클라우드 특성을 적용하는 방식
{:.lead}

**Well-Architected Framework**를 설계할 때는 가이드를 통해 일관적인 접근법을 제공하며, 총 5가지 법칙으로 나뉩니다.

<div style="text-align:center; margin-bottom:1%;">
  <img width="80%" src="https://user-images.githubusercontent.com/33611439/223372268-47afe065-d029-46ad-9494-1ac0efe26707.png">
</div>

- **Security** : 위험을 평가하고 완화하는 전략을 통해 비즈니스 가치를 제공하는 동시에 정보, 시스템 및 자산을 보호
- **Operational Excellence** : 시스템을 실행하고 운영에 대한 통찰력을 확보하여 비즈니스 가치를 제공하며, 지원 프로세스 및 절차를 지속적으로 개선
- **Reliability** : 인프라 또는 서비스 중단으로부터 복구하고 동적으로 컴퓨팅 리소스를 획득하여 수요를 충족하는 시스템의 기능을 다루며, 잘못된 구성이나 일시적인 네트워크 문제와 같은 중단 완화 기능도 다룸
- **Performance Efficiency** : computation resource를 효율적으로 사용하여 성능을 극대화하고, 수요 변화에 따라 이러한 효율성을 유지
- **Cost Optimization** : 효율성을 측정하여 불필요한 비용을 줄이기 위해 관리 서비스 사용을 고려


> <div style="display:flex">
> <img width="10%" src="https://user-images.githubusercontent.com/33611439/223784068-d782844b-0f7d-4521-8611-298620be5fbb.png">
> AWS Well-Architected Tool : AWS Service중 하나로, cloud architecture를 평가, 개선 및 설계할 때 가이드를 통해 일관적인 접근법을 제공합니다. </div>

<br>

---
## Best practices for building solutions on AWS

AWS에서 Solution을 도출하기 위해 총 10가지의 Solution Designs에 대한 **Anti-patterns**과 **Best-practices**의 사례들이 있습니다.

- ### Enable scalability
Architecture 측면에서 수요의 변화에 대처할 수 있는지 파악

<div style="text-align:center; margin-bottom:1%;">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/223797773-669501c0-8260-433a-ba3a-6df4b850bc4e.png">
</div>

Application 문제 발생 시 관리자가 직접 처리 : **Anti-pattern**
{:.figcaption}

<div style="text-align:center; margin-bottom:1%;">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/223799037-8ba030d2-71f1-44f7-84a0-fa0f5294e004.png">
</div>

Threshold를 설정 후, Application의 해당 수치 도달 시 Auto Scaling에게 Alarm 및 Scales out : **Best-practice**
{:.figcaption}

- ### Automate your environment
리소스를 모니터링하여 종료 및 구성의 자동화가 가능한지 파악

<div style="text-align:center; margin-bottom:2%;">
  <img width="90%" alt="스크린샷 2023-03-09 오전 3 37 53" src="https://user-images.githubusercontent.com/33611439/223805275-867de6c7-bc21-4928-9c70-ed03c5b1827c.png">
</div>

Application의 Error시 유저가 직접 관리자에게 알리고, 관리자가 직접 해결 : **Anti-pattern** <br>
Application Error시 CloudWatch 및 Auto Scaling의 Auto handling, 관리자에게 Alarm : **Best-practice**
{:.figcaption}

- ### Treat resource as disposable 
Resource는 언제든지 사라질 수 있고, 대체될 수 있도록 Dynamic하게 활용하여 Cloud의 이점을 가지는지 파악

|<center> Anti-Pattern </center>|<center> Best-Practice </center>|
|:-------------|:--------------|
|• Over time, different serves end up with different configurations |• Automate deployment of new resources with identical configurations |
|• Resources run when they're not needed |• Terminate resources that are not in use |
|• Hardcoded IP addresses prevent flexibility |• Swhich to new IP addresses automatically |
|• It can be difficult or inconvenient to test new updates on hardware that's in use |• Test updates on new resources, and then replace old resources with updated ones |

- ### Use loosely coupled components
독립적인 구성 요소를 가지는 Archtecture를 설계하였는지 파악

<div style="text-align: center; margin-bottom:2%">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/224224886-5c7e6161-e1bf-4374-bf4f-9859781f2a3d.png">
</div>

Component의 Scaling에 따라, 다른 Components에게 영향을 미침 : **Anti-pattern** <br>
Elastic Load Balancer(ELB)를 통해 Scaling을 관리하여 Components를 독립화 : **Best-practice**
{:.figcaption}

- ### Design services, not servers
Solution을 구할 때, Server가 필요한 이유가 타당한지 파악
  
|<center> Anti-Pattern </center>|<center> Best-Practice </center>|
|:-------------|:--------------|
|• Simple applications run on persistent servers |• When appropriate, consider using containers or a serverless solution |
|• Applications communicate directly with one another |• Message queues handle communication between applications |
|• Static web assets are stored locally on instances |• Static web assets are stored externally, such as on Amazon Simple Storage Service(Amazon S3)|
|• Backend servers handle user authentication and user state storage |• User authentication and user state storage are handled by managed AWS services |

- ### Choose the right database solution
Application environment에 대한 요구사항에 맞는 Database solution인지 파악

|Things to consider |
|:-------------|:--------------|
|• Read and write needs |• Latency requirements |
|• Total storage requirements |• Maximum concurrent users to support |
|• Typical object size and nature of access to these objects |• Nature of queries|
|• Durability requirements |• Required strength of integrity controls |

Database solution을 위한 고려사항
{:.figcaption}


- ### Avoid single points of failure
primary와 secondary DB를 두어 동기화를 통해, failure에 대해 빠른 대처가 가능한지 파악

<div style="text-align: center;">
  <img width="70%" src="https://user-images.githubusercontent.com/33611439/224239480-f46a6d99-481f-45b4-b3e2-417f8e356df0.png">
</div>

DB server의 failure 발생 시, Application server도 failure가 발생 : **Anti-pattern**
{:.figcaption}

<div style="text-align: center; margin-bottom: 2%">
  <img width="60%" src="https://user-images.githubusercontent.com/33611439/224240614-0b6d08a8-5067-4411-a70c-a7d0c60bcd93.png">
</div>

Primary와 secondary DB를 두어 data를 복제함으로써 failure에 대한 대처 진행 : **Best practice**
{:.figcaption}

- ### Optimize for cost
Cloud를 유연하게 설계할 수 있다는 이점을 활용하기 위해 효율적인 비용을 사용하는지 파악

<div style="text-align: center;">
  <table style="display: inline-block; text-align: left;">
    <thead>
      <tr>
        <th>  <center>Things to consider </center></th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td> • Are my resources the right size and type for the job? </td>
      </tr>
      <tr>
        <td> • How often will I need to use this resource? </td>
      </tr>
      <tr>
        <td> • What metrics should I monitor? </td>
      </tr>
      <tr>
        <td> • Can I replace any of my servers with managed services? </td>
      </tr>
      <tr>
        <td> • How do I make sure to turn off resources that are not in use? </td>
      </tr>
    </tbody>
  </table>
</div>


- ### Use caching
동일한 요청에 대해 Caching을 활용하여 성능 및 비용을 최적화하는지 파악

<div style="text-align: center; margin-bottom: 2%">
  <img width="90%" src="https://user-images.githubusercontent.com/33611439/224252804-1a31d665-2310-42fa-8ba0-33cee10c86e1.png">
</div>

동일한 요청의 반복적인 수행으로 인한 latency 및 cost 증가: **Anti-pattern** <br>
CloudFront를 사용하여 처음 요청 이후 Caching된 Resource는 이후 요청 시 빠르게 제공 : **Best practice**
{:.figcaption}

- ### Secure your entire infrastructure
설계한 Architecrue의 모든 Layer에 적용될 수 있는 Security 구축여부 파악

<table>
  <thead>
    <tr>
      <th colspan="2"> Things to consider</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td> • Isolate parts of your infrastructure </td>
      <td> • Use managed services </td>
    </tr>
    <tr>
      <td> • Encrypt data in transit and at rest </td>
      <td> • Log access of resources </td>
    </tr>
    <tr>
      <td> • Enforce access control granularly, using the <strong>principle of least privilege </strong> </td>
      <td> • Use multi-factor authentication(MFA) </td>
    </tr>
    <tr>
      <td > • Automate your deployments to keep security consistent </td>
    </tr>
  </tbody>
</table>

> **Principle of least privilege** : 특정 작업을 수행하는 데 필요한 최소한의 권한 집합을 적용한다는 법칙

## AWS global infrastructure

- **AWS Regions**
  - AWS Cloud infrastructure를 구성하는 요소로, AWS는 전세계에 22곳의 Region을 가짐
  - 물리적으로 존재하는 지리적 위치이며, 하나 이상의 가용영역으로 구성
  - 다른 Region과 private global network backbone으로 연결되어, 공용 인터넷과 비교했을 때 더 낮은 cost와 latency를 가짐
  - 사용자의 요구에 따라 Region간 data replication이 가능

- **AWS Availability Zones**
  - 하나 이상의 data center로 구성되며, 최대 6개의 data center를 가짐
  - 각 가용 영역은 독립적이기 때문에, Fault Isolation을 지원함
  - 특정 AWS 서비스를 사용할 때는 가용 영역을 지정 가능 (Amazon EC2 등)
  - Application을 여러 가용 영역에 분산하여 Failure situations(자연 자해 등)에서 복원력을 유지 가능

- **AWS Local Zones**
  - AWS가 지원하는 완전관리형 서비스로, latency가 매우 민감한 서비스를 위함
  - 특정 AWS 서비스를 현재 AWS Region이 존재하지 않는 대규모 인구, 산업 및 IT센터에 가깝게 배치하는 배포 유형
  - User와 Resource에 가까운 Region에서 실행가능하며, 이를 통해 latency를 최소화

- **AWS data centers**
  - 하나의 가용 영역에 존재하는 물리적인 데이터 저장 공간으로, 수 천개의 서버로 구성됨
  - 실제 데이터가 존재하고, 처리가 발생하는 공간
  - 고객에게 서비스를 제공하기 위해 항상 온라인 상태이며, 장애 발생 시 Trafic load balancing을 통해 제공받음

- **AWS Points of Presence**
  - CloudFront가 user에게 low latency으로 content를 전달하기 위해 사용하는 Global network
  - Edge Locations와 Regional Edge Cache로 구성됨
    - **Edge location** : CloudFront가 고객에게 콘텐츠를 신속하게 제공하기 위해 사용하는 데이터 센터의 네트워크
    - **Region edge cache** : Edge location에 상주하기에는 사용 빈도 수가 낮은 콘텐츠를 캐싱하는 CloudFront location으로, Origin server와 Global edge location 사이에 위치