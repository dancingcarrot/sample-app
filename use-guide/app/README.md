## Table of Contents

1. [Redis deployment 생성] (#1)
   * [1.1 Namespace 생성 ](#1-1)
   * [1.1 Redis deployment 생성 ](#1-2)
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

## <div id='1-2'/> 1.2. Redis deployment 생성
#### <div id='1-1-1'/> 1.1.1. Redis deployment 생성


---
[IMG_1_1]:../IMG/IMG_1_1.png
[IMG_1_2]:../IMG/IMG_1_2.png
[IMG_1_3]:../IMG/IMG_1_3.png
[IMG_1_4]:../IMG/IMG_1_4.png  
[IMG_1_5]:../IMG/IMG_1_5.png  
[IMG_1_6]:../IMG/IMG_1_6.png  
