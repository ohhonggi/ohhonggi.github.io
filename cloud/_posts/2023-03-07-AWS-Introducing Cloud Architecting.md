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

**Well-Architected Framework**를 설계할 때는 가이드를 통해 일관적인 접근법을 제공하며, 총 5가지 법칙으로 나뉜다.

<img width="649" src="https://user-images.githubusercontent.com/33611439/223372268-47afe065-d029-46ad-9494-1ac0efe26707.png">

- **Security** : 위험을 평가하고 완화하는 전략을 통해 비즈니스 가치를 제공하는 동시에 정보, 시스템 및 자산을 보호함
- **Operational Excellence** : 시스템을 실행하고 운영에 대한 통찰력을 확보하여 비즈니스 가치를 제공하며, 지원 프로세스 및 절차를 지속적으로 개선함
- **Reliability** : 인프라 또는 서비스 중단으로부터 복구하고 동적으로 컴퓨팅 리소스를 획득하여 수요를 충족하는 시스템의 기능을 다루며, 잘못된 구성이나 일시적인 네트워크 문제와 같은 중단 완화 기능도 다룸
- **Performance Efficiency** : computation resource를 효율적으로 사용하여 성능을 극대화하고, 수요 변화에 따라 이러한 효율성을 유지하도록 함
- **Cost Optimization** : 효율성을 측정하여 불필요한 비용을 줄이기 위해 관리 서비스 사용을 고려함


> <div style="display:flex">
> <img width="10%" src="https://user-images.githubusercontent.com/33611439/223784068-d782844b-0f7d-4521-8611-298620be5fbb.png">
> AWS Well-Architected Tool : AWS Service중 하나로, cloud architecture를 평가, 개선 및 설계할 때 가이드를 통해 일관적인 접근법을 제공함 </div>

<br>

---
## Best practices for building solutions on AWS

AWS에서 Solution을 도출하기 위한 모범 사례들

- **Enable scalability** : Architecture 측면에서 수요의 변화에 대처할 수 있는지 파악하는 사례

<img width="600" src="https://user-images.githubusercontent.com/33611439/223797773-669501c0-8260-433a-ba3a-6df4b850bc4e.png">

Application 문제 발생 시 관리자가 직접 처리 : **Anti-pattern**
{:.figcaption}

<img width="594" src="https://user-images.githubusercontent.com/33611439/223799037-8ba030d2-71f1-44f7-84a0-fa0f5294e004.png">

Threshold를 설정 후, Application의 해당 수치 도달 시 Auto Scaling에게 Alarm 및 Scales out : **Best-practice**
{:.figcaption}

- **Automate your environment** : 리소스를 모니터링하여 종료 및 구성의 자동화가 가능한지 파악하는 사례

<img width="703" alt="스크린샷 2023-03-09 오전 3 37 53" src="https://user-images.githubusercontent.com/33611439/223805275-867de6c7-bc21-4928-9c70-ed03c5b1827c.png">

Application의 Error시 유저가 직접 관리자에게 알리고, 관리자가 직접 해결 : **Anti-pattern** <br>
Application Error시 CloudWatch 및 Auto Scaling의 Auto handling, 관리자에게 Alarm : **Best-practice**
{:.figcaption}
