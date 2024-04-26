## Table of Contents

1. [Redis를 사용한 PHP 방명록 애플리케이션 배포하기](#1)
   * [1.1 Namespace 생성 ](#1-1)
   * [1.2 Redis 생성 ](#1-2)
   * [1.2.1 Redis-leader 생성 ](#1-2-1)
   * [1.2.1.1 Redis-leader deployment 생성 ](#1-2-1-1)
   * [1.2.1.2 Redis-leader service 생성 ](#1-2-1-2)
   * [1.2.2 Redis-follower 생성 ](#1-2-2)
   * [1.2.2.1 Redis-follower deployment 생성 ](#1-2-2-1)
   * [1.2.2.2 Redis-follower service 생성 ](#1-2-2-2)
   * [1.3. 방명록 프론트엔드 생성](#1-3)
   * [1.3.1. frontend deployment 생성](#1-3-1)
   * [1.3.1. frontend service 생성](#1-3-2)
   * [1.4 확인하기](#1-4)
   * [1.5 삭제하기](#1-5)
   * [1.5.1 Namespace 삭제로 전체 삭제하기](#1-5-1)
   * [1.5.2 Deployment 삭제하기](#1-5-2)
   * [1.5.3 Service 삭제하기](#1-5-3)
     

<br>

# <div id='1'/> 1. Redis를 사용한 PHP 방명록 애플리케이션 배포하기
본 장에서는 Redis를 사용한 PHP 방명록 애플리케이션 배포에 대한 설명을 기술하였다.

<br>

## <div id='1-1'/> 1.1. Namespace 생성
#### <div id='1-1-1'/> 1.1.1. Namespace 생성
- Clusters 메뉴의 Namespaces를 클릭하여 Namespace 목록 페이지로 이동한다.
- Namespace 목록에서 생성 버튼을 클릭하여 Namespace 생성 페이지로 이동한다.
  ![IMG_1_1]

<br>


- Name 작성 박스에 지정할 Namespace명을 입력한다.
  ![IMG_1_2]

<br>

- Namespace 생성 페이지에서 Resource Quotas를 선택해 cp-medium-resourcequota 를 선택하고 선택 완료 버튼을 클릭한다.
  ![IMG_1_3]

<br>

- Namespace 생성 페이지에서 Limit Ranges를 선택해 cp-medium-limitrange 를 선택하고 선택 완료 버튼을 클릭한다.

  ![IMG_1_4]

<br>

- Name, Resource Quotas, Limit Ranges가 모두 설정이 되었는지 확인 후 저장 버튼을 클릭한다

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

- 생성 버튼을 클릭 후 Yaml 작성박스에 Redis-leader deployment를 생성하는 yaml을 작성하고 저장 버튼을 클릭한다.
  ![IMG_2_3]

<br>

- redis-leader deployment가 생성되었는지 확인한다.
  ![IMG_2_4]

<br>

#### <div id='1-2-1-2'/> 1.2.1.2. Redis-leader service 생성
- Services 메뉴의 Services를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_5]

<br>

- Yaml 작성 박스에 redis-leader service yaml을 작성한 후 저장 버튼을 클릭한다.
  ![IMG_2_6]
  
<br>

- 생성한 서비스가 올라갔는지 확인한다.
  ![IMG_2_7]
  
<br>

### <div id='1-2-2'/> 1.2.2. Redis-follower 생성
#### <div id='1-2-2-1'/> 1.2.2.1. Redis-follower deployment 생성
- Workloads 메뉴의 Deployment를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_8]
  
<br>
  
- Yaml 작성 박스에 Redis-follower deploymnet yaml을 작성한 후 저장 버튼을 클릭한다.
  ![IMG_2_9]

<br>

- Redis-follower deployment가 올라갔는지 확인한다.
  ![IMG_2_10]
  
<br>

#### <div id='1-2-2-2'/> 1.2.2.2. Redis-follower service 생성

- Services 메뉴의 Services를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_11]

<br>

- Yaml 작성 박스에 Redis-follower service yaml을 작성한 후 저장 버튼을 클릭한다.
  ![IMG_2_12]
  
<br>

- 화면에서 Redis-follower service가 올라갔는지 확인한다.
  ![IMG_2_13]

<br>

## <div id='1-3'/> 1.3. 방명록 프론트엔드 생성
#### <div id='1-3-1'/> 1.3.1. frontend deployment 생성

- Workloads 메뉴의 Deployment 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_3_1]
  
<br>

- Yaml 작성 박스에 frontend deployment yaml을 작성하고 저장버튼을 클릭한다.
  ![IMG_3_2]
  
  <br>
  
- 화면에서 frontend deployment가 올라갔는지 확인한다.
  ![IMG_3_3]
  
  <br>
  

#### <div id='1-3-2'/> 1.3.2. frontend service 생성

- Services 메뉴의 Services를 선택한 후 생성 버튼을 클릭한다.
  ![IMG_3_4]
  
<br>

- Yaml 작성 박스에 frontend service yaml을 작성하고 확인 버튼을 클릭한다.
  ![IMG_3_5]

<br>

- 화면에서 서비스가 등록된 것을 확인한다.
  ![IMG_3_6]

<br>

## <div id='1-4'/> 1.4. 확인하기

  
- Services 메뉴의 Services에서 frontend 서비스의 port를 확인한다.
  ![IMG_4_3]

<br>
  
- 브라우저에 http://{node public ip}:{service port} 를 작성한다.


<br>
  
- 동일한 화면이 나타나는지 확인한다.
  ![IMG_4_5]

<br>


## <div id='1-5'/> 1.5. 삭제하기
#### <div id='1-5-1'/> 1.5.1. Namespace 삭제로 전체 삭제하기

- Clusters에서 Namespace을 클릭하고 생성했던 Namespace를 클릭한다.
  
  ![IMG_8_1]
  
  ![IMG_8_2]
  
  <br>
- 화면 하단의 삭제 버튼을 클릭하면 생성했던 service 및 deployment가 삭제된다.
  
  ![IMG_8_3]
  
<br>

#### <div id='1-5-2'/> 1.5.2. Deployment 삭제하기

- Workloads 메뉴에서 Deployment를 선택하고 생성했던 deployment명을 클릭한다.
  ![IMG_7_1]
  
<br>

- 화면 하단의 삭제 버튼을 클릭하면 생성했던 deployment가 삭제된다.
 
 ![IMG_7_3]
 
<br>

#### <div id='1-5-3'/> 1.5.3. Service 삭제하기
- Services 메뉴에서 Services를 선택해 생성했던 service명을 클릭한다.
  ![IMG_6_1]

  <br>
  
- 화면 하단의 삭제 버튼을 클릭하면 생성했던 service가 삭제된다.
 
  ![IMG_6_3]

<br>
---
<br>

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
[IMG_3_1]:../IMG/IMG_3_1.png
[IMG_3_2]:../IMG/IMG_3_2.png
[IMG_3_3]:../IMG/IMG_3_3.png
[IMG_3_4]:../IMG/IMG_3_4.png
[IMG_3_5]:../IMG/IMG_3_5.png
[IMG_3_6]:../IMG/IMG_3_6.png
[IMG_4_1]:../IMG/IMG_4_1.png
[IMG_4_2]:../IMG/IMG_4_2.png
[IMG_4_3]:../IMG/IMG_4_3.png
[IMG_5_1]:../IMG/IMG_5_1.png
[IMG_4_5]:../IMG/IMG_4_5.png
[IMG_8_1]:../IMG/IMG_8_1.png
[IMG_8_2]:../IMG/IMG_8_2.png
[IMG_8_3]:../IMG/IMG_8_3.png
[IMG_6_1]:../IMG/IMG_6_1.png
[IMG_6_2]:../IMG/IMG_6_2.png
[IMG_6_3]:../IMG/IMG_6_3.png
[IMG_7_1]:../IMG/IMG_7_1.png
[IMG_7_2]:../IMG/IMG_7_2.png
[IMG_7_3]:../IMG/IMG_7_3.png


