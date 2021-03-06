---
layout: single
title:  "Django의 핵심기능 03 - Template System 05 - auto HTML escape "
---

MTV 방식에서 템플릿 시스템의 HTML escape 내용이 계속 헷갈렸다. 그 이유는, 렌더링의 결과인 템플릿 파일과 웹브라우저의 해석 결과인 최종 화면을 혼동했기 때문이다. 템플릿 코드는 두 번의 해석을 거친다는 점을 염두하고 HTML escape를 이해하자.



### 장고 프로젝트의 템플릿 코드가 사용자에게 보여지기까지의 과정

1. 템플릿 코드 : 렌더링 전의 HTML 코드와 장고의 템플릿 코드
2. 렌더링 : 템플릿 코드(1번)를 해석하는 과정으로, 이때 변수에 들어있는 HTML 태그는 auto escape 됨
3. 템플릿 파일 : 렌더링(2번)의 결과물로 나오는 단순한 텍스트 파일(HTML, XML, JSON 등)
4. 웹 브라우저 : HTML 파일(3번)을 해석하여 화면을 나타내는, 대표적인 웹 클라이언트
5. 최종 화면 :  웹 브라우저(4번)이 보여주는, 사용자가 보게 되는 화면



### HTML 태그가 들어있는 변수가 있을 때, auto HTML escape를 ON/OFF하는 경우

| Process                | autoescape on                                                | autoescape off                                               |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 0. 생성된 변수 (.py)   | name = "\<b>username"                                        | name = "\<b>username"                                        |
| 1. 템플릿 코드         | Hello, \{\{ name \}\}                                        | Hello, \{\{ name \}\}                                        |
| 2. 렌더링 과정         | 변수 값에 있는 HTML 태그를 탈출문자로 변경함                 | 변수 값에 있는 HTML 태그를 탈출문자로 변경하지 않음          |
| 3. 템플릿 파일 (.html) | 템플릿 파일에 탈출문자가 나타남 <br />예시 : Hello, &#38;lt;b&#38;gt;username | 템플릿 파일에 HTML 태그가 나타남<br />예시 : Hello, \<b>username |
| 4. 웹 브라우저의 해석  | 템플릿 파일의 탈출문자를 해석함                              | 템플릿 파일의 HTML 태그를 해석함                             |
| 5. 최종 화면           | 탈출문자가 해석된 결과로 단순 특수문자가 화면에 출력됨<br />예시 : Hello, \<b>username | HTML 태그가 해석된 결과로 태그 기능이 적용된 화면이 출력됨<br />예시 : Hello, **username** |
| 결론                   | 사용자가 입력한 데이터를 그대로 렌더링하는 위험을 방지하기 위해, 즉 XSS 공격을 방지하기 위해<br />**템플릿 태그로 on하지 않아도 장고가 자동 이스케이프 기능을 제공함** | 입력받은 데이터를 그대로 렌더링하도록 하면, 악성 스크립트를 전송하여 사이트를 공격하는 XSS 공격에 취약해짐<br />**따라서, 안전한 경우에만 템플릿 태그로 autoescape를 해제함** |
| 용례                   |                                                              |                                                              |



> 참고 자료 : [Django HTML 코드가 이스케이프 되었을때, 템플릿에서 html 태그로 인식하게 만들기](https://magento4.com/django-html-%EC%BD%94%EB%93%9C%EA%B0%80-%EC%9D%B4%EC%8A%A4%EC%BC%80%EC%9D%B4%ED%94%84-%EB%90%98%EC%97%88%EC%9D%84%EB%95%8C/)



> ### 용례에 대한 추가 공부 필요
>
> *책에서 분명, 사용자가 입력한 데이터를 그대로 렌더링할 때의 위험성 때문에 자동 이스케이프 기능을 제공한다고 했는데....*
> *왜 다음과 같은 상황에서 자동이스케이프 기능을 비활성화해야한다고 했지?* 
>
> 1. *HTML 태그를 그대롤 출력하고 싶은 경우 : 자동 이스케이프 기능을 ON 해야하는 거 아닌가?*
> 2. *이스케이프 문자가 들어있는 이메일 메시지를 템플릿 파일에 출력하는 경우 : 이건 뭐지?*

