## Table of Contents

1. [Redis를 사용한 PHP 방명록 애플리케이션 배포하기](#1)
   * [1.1 Redis 생성 ](#1-1)
   * [1.1.1 Redis-leader 생성 ](#1-1-1)
   * [1.1.1.1 Redis-leader deployment 생성 ](#1-1-1-1)
   * [1.1.1.2 Redis-leader service 생성 ](#1-1-1-2)
   * [1.1.2 Redis-follower 생성 ](#1-1-2)
   * [1.1.2.1 Redis-follower deployment 생성 ](#1-1-2-1)
   * [1.1.2.2 Redis-follower service 생성 ](#1-1-2-2)
   * [1.2. 방명록 프론트엔드 생성](#1-2)
   * [1.2.1. frontend deployment 생성](#1-2-1)
   * [1.2.1. frontend service 생성](#1-2-2)
   * [1.3 확인하기](#1-3)
2. [삭제하기(참고)](#2)
   * [2.1 Redis-leader 삭제하기](#2-1)
   * [2.1.1 Redis-leader Service 삭제하기](#2-1-1)
   * [2.1.2 Redis-leader Deployment 삭제하기](#2-1-2)
   * [2.2. Redis-follower 삭제하기](#2-2)
   * [2.2.1 Redis-follower Service 삭제하기](#2-2-1)
   * [2.2.2 Redis-follower Deployment 삭제하기](#2-2-2)
   * [2.3. Frontend 삭제하기](#2-3)
   * [2.3.1 Frontend Service 삭제하기](#2-3-1)
   * [2.3.2 Frontend Deployment 삭제하기](#2-3-2)
     

<br>

# <div id='1'/> 1. Redis를 사용한 PHP 방명록 애플리케이션 배포하기
본 장에서는 Redis를 사용한 PHP 방명록 애플리케이션 배포에 대한 설명을 기술하였다.

<br>

## <div id='1-1'/> 1.1. Redis 생성
### <div id='1-1-1'/> 1.1.1. Redis-leader 생성
#### <div id='1-1-1-1'/> 1..1.1. Redis-leader deployment 생성

- Workloads 메뉴의 Deployment 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_2]

<br>

- Yaml 작성박스에 하단의 Redis-leader deployment yaml을 입력하고 저장 버튼을 클릭한다.
  ![IMG_2_3]
  
<br>

#### Redis-leader deployment 

``` bash

apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-leader
  labels:
    app: redis
    role: leader
    tier: backend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
        role: leader
        tier: backend
    spec:
      containers:
      - name: leader
        image: "docker.io/redis:6.0.5"
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 6379
```
<br>

- redis-leader deployment가 생성되었는지 확인한다.
  ![IMG_2_4]

<br>

#### <div id='1-1-1-2'/> 1.1.1.2. Redis-leader service 생성
- Services 메뉴의 Services를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_5]

<br>

- Yaml 작성박스에 하단의 Redis-leader service yaml을 입력하고 저장 버튼을 클릭한다.
  ![IMG_2_6]

<br>

#### Redis-leader Service 

```bash

apiVersion: v1
kind: Service
metadata:
  name: redis-leader
  labels:
    app: redis
    role: leader
    tier: backend
spec:
  ports:
  - port: 6379
    targetPort: 6379
  selector:
    app: redis
    role: leader
    tier: backend
```

<br>

- 서비스가 생성되었는지 확인한다.
  <br>
  ![IMG_2_7]
  
<br>

### <div id='1-1-2'/> 1.1.2. Redis-follower 생성
#### <div id='1-1-2-1'/> 1.1.2.1. Redis-follower deployment 생성
- Workloads 메뉴의 Deployment를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_8]
  
<br>
  
- Yaml 작성박스에 하단의 Redis-follower deployment yaml을 입력하고 저장 버튼을 클릭한다.
  ![IMG_2_9]

  <br>
  
#### Redis-follower deployment 

```bash

apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-follower
  labels:
    app: redis
    role: follower
    tier: backend
spec:
  replicas: 2
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
        role: follower
        tier: backend
    spec:
      containers:
      - name: follower
        image: gcr.io/google_samples/gb-redis-follower:v2
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 6379
```
<br>



- Redis-follower deployment가 생성되었는지 확인한다.
  <br>
  ![IMG_2_10]
  
<br>

#### <div id='1-1-2-2'/> 1.1.2.2. Redis-follower service 생성

- Services 메뉴의 Services를 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_2_11]

<br>

- Yaml 작성박스에 하단의 Redis-follower service yaml을 입력하고 저장 버튼을 클릭한다.
  ![IMG_2_12]

<br>

#### Redis-follower service 

```bash

apiVersion: v1
kind: Service
metadata:
  name: redis-follower
  labels:
    app: redis
    role: follower
    tier: backend
spec:
  ports:
    # the port that this service should serve on
  - port: 6379
  selector:
    app: redis
    role: follower
    tier: backend
```
  
<br>

- 화면에서 Redis-follower service가 생성되었는지 확인한다.
  ![IMG_2_13]

<br>

## <div id='1-2'/> 1.2. 방명록 프론트엔드 생성
#### <div id='1-2-1'/> 1.2.1. frontend deployment 생성

- Workloads 메뉴의 Deployment 클릭한 후 생성 버튼을 클릭한다.
  ![IMG_3_1]
  
<br>

- Yaml 작성박스에 하단의 frontend deployment yaml을 입력하고 저장 버튼을 클릭한다.
  <br>
  ![IMG_3_2]

<br>

#### frontend deployment 

```bash

apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
        app: guestbook
        tier: frontend
  template:
    metadata:
      labels:
        app: guestbook
        tier: frontend
    spec:
      containers:
      - name: php-redis
        image: corelab/gb-frontend:v5
        env:
        - name: GET_HOSTS_FROM
          value: "dns"
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 80
```
  <br>
  
- 화면에서 frontend deployment가 생성되었는지 확인한다.
  <br>
  ![IMG_3_3]
  
  <br>
  

#### <div id='1-2-2'/> 1.2.2. frontend service 생성

- Services 메뉴의 Services를 선택한 후 생성 버튼을 클릭한다.
  <br>
  ![IMG_3_4]
  
<br>

- Yaml 작성박스에 하단의 frontend service yaml을 입력하고 저장 버튼을 클릭한다.
  <br>
  ![IMG_3_5]

  <br>
  
#### frontend service 

```bash

apiVersion: v1
kind: Service
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  type: NodePort
  ports:
  - port: 80
  selector:
    app: guestbook
    tier: frontend
```
<br>

- 화면에서 서비스가 등록된 것을 확인한다.
  <br>
  ![IMG_3_6]

<br>

## <div id='1-3'/> 1.3. 확인하기

  
- Services 메뉴의 Services에서 frontend 서비스의 port를 확인한다.
  <br>
  ![IMG_4_3]

<br>
  
- 브라우저에 http://{node public ip}:{service port} 를 작성한다.
  + playpark로 배포시 예시 ) http://playpark-cp.k-paas.org:30705/


<br>
  
- 동일한 화면이 나타나는지 확인한다.
  <br>
  ![IMG_4_5]

<br>


# <div id='2'/> 2. 삭제하기(참고)
### <div id='2-1'/> 2.1. Redis-leader 삭제하기
#### <div id='2-1-1'/> 2.1.1. Redis-leader Service 삭제하기

- Services메뉴에서 Services를 선택한 후 redis-leader를 클릭한다.
  <br>
  ![IMG_9_1]
  
  <br>
- 화면 하단의 삭제 버튼을 클릭하여 redis-leader service를 삭제한다.
  <br>
  ![IMG_9_2]


  <br>
- List에서 redis-leader service가 삭제되었는지 확인한다.
  <br>
  ![IMG_9_5]
<br>

#### <div id='2-1-2'/> 2.1.2. Redis-leader Deployment 삭제하기

-  Workloads메뉴에서 Deployment를 선택한 후 redis-leader를 클릭한다.
  ![IMG_10_1]

<br>
- 화면 하단의 삭제 버튼을 클릭하여 redis-leader deployment를 삭제한다.

![IMG_10_2]


<br>

- List에서 redis-leader deployment가 삭제되었는지 확인한다.

![IMG_10_5]

<br>

### <div id='2-2'/> 2.2. Redis-follower 삭제하기
#### <div id='2-2-1'/> 2.2.1. Redis-follower Service 삭제하기

- Services메뉴에서 Services를 선택한 후 redis-follower를 클릭한다.
  <br>
  ![IMG_11_1]
  <br>

- 화면 하단의 삭제 버튼을 클릭하여 redis-follower service를 삭제한다.
  <br>
  ![IMG_11_2]

  <br>

- List에서 redis-follower service가 삭제되었는지 확인한다.
  ![IMG_11_5]

<br>

#### <div id='2-2-2'/> 2.2.2. Redis-follower Deployment 삭제하기

-  Workloads메뉴에서 Deployment를 선택한 후 redis-follower를 클릭한다.
   <br>
  ![IMG_12_1]

<br>

- 화면 하단의 삭제 버튼을 클릭하여 redis-follower deployment를 삭제한다.
  <br>
  ![IMG_12_2]


<br>

- List에서 redis-follower deployment가 삭제되었는지 확인한다.
  <br>
  ![IMG_12_5]

<br>

### <div id='2-3'/> 2.3. frontend 삭제하기
#### <div id='2-3-1'/> 2.3.1. frontend Service 삭제하기

- Services메뉴에서 Services를 선택한 후 frontend를 클릭한다.
  <br>
  ![IMG_13_1]
<br>

- 화면 하단의 삭제 버튼을 클릭하여 frontednd service를 삭제한다.
  <br>
  ![IMG_13_2]
<br>

- List에서 frontend servcie가 삭제되었는지 확인한다.
  <br>
  ![IMG_13_5]
  <br>

#### <div id='2-3-2'/> 2.3.2. frontend Deployment 삭제하기

-  Workloads메뉴에서 Deployment를 선택한 후 frontend를 클릭한다.
  ![IMG_14_1]
  
  <br>

- 화면 하단의 삭제 버튼을 클릭하여 frontend deployment를 삭제한다.
  <br>
  ![IMG_14_2]

<br>

- List에서 frontend deployment가 삭제되었는지 확인한다.
  <br>
  ![IMG_14_5]

<br>

---


[IMG_1_1]:../images/sample_stateless/IMG_1_1.png
[IMG_1_2]:../images/sample_stateless/IMG_1_2.png
[IMG_1_3]:../images/sample_stateless/IMG_1_3.png
[IMG_1_4]:../images/sample_stateless/IMG_1_4.png  
[IMG_1_5]:../images/sample_stateless/IMG_1_5.png  
[IMG_1_6]:../images/sample_stateless/IMG_1_6.png
[IMG_2_1]:../images/sample_stateless/IMG_2_1.png
[IMG_2_2]:../images/sample_stateless/IMG_2_2.png
[IMG_2_3]:../images/sample_stateless/IMG_2_3.png
[IMG_2_4]:../images/sample_stateless/IMG_2_4.png
[IMG_2_5]:../images/sample_stateless/IMG_2_5.png
[IMG_2_6]:../images/sample_stateless/IMG_2_6.png
[IMG_2_7]:../images/sample_stateless/IMG_2_7.png
[IMG_2_8]:../images/sample_stateless/IMG_2_8.png
[IMG_2_9]:../images/sample_stateless/IMG_2_9.png
[IMG_2_10]:../images/sample_stateless/IMG_2_10.png
[IMG_2_11]:../images/sample_stateless/IMG_2_11.png
[IMG_2_12]:../images/sample_stateless/IMG_2_12.png
[IMG_2_13]:../images/sample_stateless/IMG_2_13.png
[IMG_3_1]:../images/sample_stateless/IMG_3_1.png
[IMG_3_2]:../images/sample_stateless/IMG_3_2.png
[IMG_3_3]:../images/sample_stateless/IMG_3_3.png
[IMG_3_4]:../images/sample_stateless/IMG_3_4.png
[IMG_3_5]:../images/sample_stateless/IMG_3_5.png
[IMG_3_6]:../images/sample_stateless/IMG_3_6.png
[IMG_4_1]:../images/sample_stateless/IMG_4_1.png
[IMG_4_2]:../images/sample_stateless/IMG_4_2.png
[IMG_4_3]:../images/sample_stateless/IMG_4_3.png
[IMG_5_1]:../images/sample_stateless/IMG_5_1.png
[IMG_4_5]:../images/sample_stateless/IMG_4_5.png
[IMG_8_1]:../images/sample_stateless/IMG_8_1.png
[IMG_8_2]:../images/sample_stateless/IMG_8_2.png
[IMG_8_3]:../images/sample_stateless/IMG_8_3.png
[IMG_6_1]:../images/sample_stateless/IMG_6_1.png
[IMG_6_2]:../images/sample_stateless/IMG_6_2.png
[IMG_6_3]:../images/sample_stateless/IMG_6_3.png
[IMG_7_1]:../images/sample_stateless/IMG_7_1.png
[IMG_7_2]:../images/sample_stateless/IMG_7_2.png
[IMG_7_3]:../images/sample_stateless/IMG_7_3.png
[IMG_9_1]:../images/sample_stateless/IMG_9_1.png
[IMG_9_2]:../images/sample_stateless/IMG_9_2.png
[IMG_9_3]:../images/sample_stateless/IMG_9_3.png
[IMG_9_4]:../images/sample_stateless/IMG_9_4.png
[IMG_9_5]:../images/sample_stateless/IMG_9_5.png
[IMG_10_1]:../images/sample_stateless/IMG_10_1.png
[IMG_10_2]:../images/sample_stateless/IMG_10_2.png
[IMG_10_3]:../images/sample_stateless/IMG_10_3.png
[IMG_10_4]:../images/sample_stateless/IMG_10_4.png
[IMG_10_5]:../images/sample_stateless/IMG_10_5.png
[IMG_11_1]:../images/sample_stateless/IMG_11_1.png
[IMG_11_2]:../images/sample_stateless/IMG_11_2.png
[IMG_11_3]:../images/sample_stateless/IMG_11_3.png
[IMG_11_4]:../images/sample_stateless/IMG_11_4.png
[IMG_11_5]:../images/sample_stateless/IMG_11_5.png
[IMG_12_1]:../images/sample_stateless/IMG_12_1.png
[IMG_12_2]:../images/sample_stateless/IMG_12_2.png
[IMG_12_3]:../images/sample_stateless/IMG_12_3.png
[IMG_12_4]:../images/sample_stateless/IMG_12_4.png
[IMG_12_5]:../images/sample_stateless/IMG_12_5.png
[IMG_13_1]:../images/sample_stateless/IMG_13_1.png
[IMG_13_2]:../images/sample_stateless/IMG_13_2.png
[IMG_13_3]:../images/sample_stateless/IMG_13_3.png
[IMG_13_4]:../images/sample_stateless/IMG_13_4.png
[IMG_13_5]:../images/sample_stateless/IMG_13_5.png
[IMG_14_1]:../images/sample_stateless/IMG_14_1.png
[IMG_14_2]:../images/sample_stateless/IMG_14_2.png
[IMG_14_3]:../images/sample_stateless/IMG_14_3.png
[IMG_14_4]:../images/sample_stateless/IMG_14_4.png
[IMG_14_5]:../images/sample_stateless/IMG_14_5.png
