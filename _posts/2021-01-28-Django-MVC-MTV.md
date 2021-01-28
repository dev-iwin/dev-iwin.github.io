---
layout: single
title:  "Django와 MVC 패턴, MTV 패턴"
---

## MVC 패턴이란?

MVC 패턴은 소프트웨어 개발 방법론 중 하나로 소프트웨어를 Model, View, Controller의 역할로 구분하여 개발하는 방법이다. MVC 각 부분이 서로에게 영향이 없도록 하면서 시스템을 개발하고 유지 보수할 수 있는 장점[1]이 있다. (물론 Model과 View가 완벽히 분리 할 수 없기 때문에 패턴이 모호해질 수 있고 변형이 올 수 있다는 단점도 있다고 한다.)

1. Model : 데이터베이스, 애플리케이션의 정보 등을 담는 데이터 집합소
2. View : 사용자에게 보이는 화면 정보를 보유하고 나타냄
3. Controller : Model과 View를 컨트롤하는, 사용자와 서버 간의 인터페이스 역할

웹에서 로그인 하는 과정으로 MVC 패턴을 설명하면 다음과 같다.

| MVC 패턴                                           | Web에서 로그인                                          |
| -------------------------------------------------- | ------------------------------------------------------- |
| 사용자가 View을 통해 Controller에 요청             | 사용자가 ID, PW를 입력                                  |
| Controller는 내부적으로 특정한 처리 진행           | Controller가 ID, PW 받음                                |
| Controller는 필요 시 Model에서 데이터를 가져옴     | 데이터베이스에서 ID, PW 확인                            |
| Controller가 처리된 결과를 다시금 View에 보이게 함 | 확인 결과에 따라 로그인 화면,<br /> or 로그인 실패 화면 |



## MTV 패턴은?

MVC 패턴과 비슷한 디자인 패턴으로, MVC 패턴에서 이야기하는 Controller의 역할을 Framework 자체에서 수행하는 Django의 방식을 더 잘 설명하는 패턴이라고 한다.(출처 : [위키피디아](https://ko.wikipedia.org/wiki/%EC%9E%A5%EA%B3%A0_(%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)), [Django 공홈 문서](https://docs.djangoproject.com/ko/3.1/glossary/) )

[MTV 방식의 장점](https://onsil-thegreenhouse.github.io/programming/django/web_programmig/2017/09/15/django_tutorial_ch1-1/)은 다음과 같다. (*MVC 방식 장점과 동일하다고 봐야하는 듯하다.*)

1. 모델, 템플릿, 뷰 각각의 모듈간에 독립성을 유지 가능
2. 소프트웨어 개발의 중요 원칙인 [느슨한 결합(Loose Coupling) 설계 원칙](https://hongjinhyeon.tistory.com/141)에도 부합
3. 디자이너, 프론트개발자, 백엔드 개발자 간의 협업 용이



## Django에서의 MVC 패턴과 MTV 패턴

Django와 MVC 패턴, MTV 패턴은 다음과 같이 매칭된다.

|  MVC 패턴  | MTV패턴  | Django Poject의 관련 파일 및 폴더 |
| :--------: | :------: | :-------------------------------: |
|   Model    |  Model   |             models.py             |
|    View    | Template |          templates 폴더           |
| Controller |   View   |             Views.py              |

1. models.py
   
   * 위치 : Django 프로젝트 폴더 > 하위에 동명의 폴더 > 하위에 생성한 app 폴더 내부에 있음
   
   * 사용법 : models.py 파일에  class로 테이블의 형태를 정의함
   
     > '모델'이란 간단히 말하면 데이터베이스에서의 '테이블', 즉 '데이터를 가진 하나의 묶음'이라 할 수 있고, 그 데이터의 형태에 대해 models.py 에서 class로 정의함.
   
2. templates 폴더

   * 위치 : 생성한 app폴더 내부에 templates 폴더 직접 생성

   * 사용법 : templates 폴더 하위에 app 폴더와 동명의 폴더 생성한 뒤, 거기에 html 등 파일 작성

     > 하위에 동명의 폴더를 또 생성하는 이유는 동일한 이름의 파일을 가질 때 생길 수 있는 문제를 막기 위한 것이라고 함. (*파일을 참조해올 때 같은 이름의 파일이 여러 폴더에 있으면, 어느 폴더의 파일을 가져오라는 것인지 모호해지기 때문인 듯함.*)

3. Views.py

   * 위치 : Django 프로젝트 폴더 > 하위에 동명의 폴더 > 하위에 생성한 app 폴더 내부에 있음

   * 사용법 : Views.py 파일에 template 역할을 하는 파일들에서 사용할 함수를 정의함

     > 참고로 내가 했던 To Do List 웹페이지 프로젝트에서는, app폴더의 urls.py가 사용자의 요청을Views.py(Controller)로 넘기는 역할을 함. Django 프로젝트 폴더 하위에 동명의 폴더에도 urls.py가 있는데, 이는 첫 화면(메인 페이지)에 대해서만 처리를 넘겼고, 그 후로는 쭉 app 폴더의 urls.py가 액션에 따라 넘김.

   

___

전반적인 내용의 출처 : 책 <Django 한그릇 뚝딱>