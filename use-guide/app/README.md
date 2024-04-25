## Table of Contents

1. [Redis deployment 생성] (#1)
   * [1.1 Namespace 생성 ](#1-1)
   * [1.2 Redis 생성 ](#1-2)
   * [1.2.1 Redis deployment 생성](#1-2-1)
   * [1.2.2 Redis service 생성](#1-2-1)
<br>

# <div id='1'/> 1. Redis를 사용한 PHP 방명록 애플리케이션 배포하기
본 장에서는 Redis를 사용한 PHP 방명록 애플리케이션 배포에 대한 설명을 기술하였다.

<br>

## <div id='1-1'/> 1.1. Namespace 생성
#### <div id='1-1-1'/> 1.1.1. Namespace 생성
- Clusters 메뉴의 Namespaces 클릭하여 Namespace 목록 페이지로 이동한다.
  ![IMG_1_1]

<br>

- Namespace 목록에서 생성 버튼을 클릭하여 Namespace 생성 페이지로 이동한다.
- Name에 지정할 Namespace의 name을 입력한다.
  ![IMG_1_2]

<br>

- Namespace 생성 페이지에서 Resource Quotas를 선택해 cp-medium-resourcequota 를 선택하고 선택 완료 버튼을 누른다.
  ![IMG_1_3]

<br>
- Namespace 생성 페이지에서 Limit Ranges를 선택해 cp-medium-limitrange 를 선택하고 선택 완료 버튼을 누른다.
  ![IMG_1_4]

<br>
- Namespace, Resource Quotas, Limit Ranges가 모두 설정이 되었는지 확인 후 저장 버튼을 누른다.
  ![IMG_1_5]

  <br>
- Namespace list 목록에 자신이 생성한 Namespace가 생성되었는지 확인한다.
  ![IMG_1_6]

<br>

## <div id='1-2'/> 1.2. Redis 생성
### <div id='1-2-1'/> 1.2.1. Redis-leader 생성
#### <div id='1-2-1-1'/> 1.2.1.1. Redis-leader deployment 생성

- Workloads 메뉴의 Deployment 클릭한 후 상단의 ALL을 선택하고 생성한 Namespace명을 선택한다.
  ![IMG_2_1]
  ![IMG_2_2]

<br>

- 생성 화면을 누른 후 Yaml 작성박스에 Redis deployment를 생성하는 yaml을 작성하고 저장 버튼을 누른다.
  ![IMG_2_3]

<br>

- Redis deployment가 생성되었는지 확인한다.
  ![IMG_2_4]

<br>

#### <div id='1-2-1-2'/> 1.2.1.2. Redis service 생성
- Services 메뉴의 Services를 클릭한 후 생성 버튼을 누른다.
  ![IMG_2_5]

<br>

- Yaml 작성 박스에 Redis service yaml을 작성한 후 저장 버튼을 누른다.
  ![IMG_2_6]
  
<br>

- 생성한 서비스가 잘 올라갔는지 확인한다.
  ![IMG_2_7]
  
<br>

### <div id='1-2-2'/> 1.2.2. Redis-follower 생성
#### <div id='1-2-2-1'/> 1.2.2.1. Redis-follower deployment 생성
- Workloads 메뉴의 Deployment 클릭한 후 선택 생성 버튼을 누른다.
  ![IMG_2_8]
<br>
  
- Yaml 작성 박스에 Redis-follower deploymnet yaml을 작성한 후 저장 버튼을 누른다.
  ![IMG_2_9]

<br>
- Redis-follower deployment가 올라갔는지 확인한다.
  ![IMG_2_10]
<br>
#### <div id='1-2-2-1'/> 1.2.2.1. Redis-follower service 생성

- Services 메뉴의 Services를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_11]

<br>
- Yaml 작성 박스에 Redis-follower service yaml을 작성한 후 저장 버튼을 클릭한다.
  ![IMG_2_12]
<br>
- 화면에서 Redis-follower service가 잘 올라갔는지 확인한다.
  ![IMG_2_13]
---
[IMG_1_1]:../IMG/IMG_1_1.png
[IMG_1_2]:../IMG/IMG_1_2.png
[IMG_1_3]:../IMG/IMG_1_3.png
[IMG_1_4]:../IMG/IMG_1_4.png  
[IMG_1_5]:../IMG/IMG_1_5.png  
[IMG_1_6]:../IMG/IMG_1_6.png
[IMG_2_1]:../IMG/IMG_2_1.png
[IMG_2_2]:../IMG/IMG_2_2.png
[IMG_2_3]:../IMG/IMG_2_3.png
[IMG_2_4]:../IMG/IMG_2_4.png
[IMG_2_5]:../IMG/IMG_2_5.png
[IMG_2_6]:../IMG/IMG_2_6.png
[IMG_2_7]:../IMG/IMG_2_7.png
[IMG_2_8]:../IMG/IMG_2_8.png
[IMG_2_9]:../IMG/IMG_2_9.png
[IMG_2_10]:../IMG/IMG_2_10.png
[IMG_2_11]:../IMG/IMG_2_11.png
[IMG_2_12]:../IMG/IMG_2_12.png
[IMG_2_13]:../IMG/IMG_2_13.png
