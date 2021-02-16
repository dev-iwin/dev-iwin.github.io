---
layout: single
title:  "Django 핵심기능 04 - Form 처리하기"
---



### 웹 개발에서의 폼이라는 용어

: 폼은 사용자로부터 입력을 받기 위해 사용. (예 :텍스트 입력, 항목 선택)

1. HTML의 `<form>`을 지칭
2. `<form>`을 만들어내는 장고의 Form 클래스를 지칭
3. 서버로 제출된 구조화된 데이터를 지칭
4. 1~3번을 모두 통칭

### HTML의 폼 : `<form>...</form>` 사이에 있는 요소들의 집합

1. input 태그 : 필수적인 요소
2. action 속성 : 폼 데이터를 보낼 곳, 즉 URL을 지정
3. method 속성 : HTML에서는 HTTP 프로토콜 중 GET 또는 POST만 가능한데, 장고에서는 폼의 데이터를 보낼 때 POST 방식만 사용
4. CSRF 방지 기능 : 장고에서 제공해주는 `{% csrf_token %}` 템플릿 태그

### 웹 서버에서의 일반적인 폼 처리

: 복잡하지만, 공통적인 절차가 있음 (예: Admin 사이트)

1. 폼 화면 출력용의 여러 타입의 여러 위젯을 준비
2. HTML로 렌더링
3. 적절한 인터페이스를 사용하여 폼에 데이터를 입력 및 수정
4. 폼 데이터를 서버로 전송
5. 서버에서 데이터가 유효한지 검증
6. 처리를 위해 저장되거나 전달

### 폼 처리를 위한 장고의 기능

1. 폼 생성에 필요한 데이터를 폼 클래스로 구조화하기
2. 폼 클래스의 데이터를 렌더링하여 HTML 폼 만들기
3. 사용자로부터 제출된 폼과 데이터를 수신하고 처리하기

### 장고의 폼 클래스 

> cf. 모델 클래스
>
> 1. DB 테이블의 논리 구조와 동작, 사용자에게 보여지는 방식들을 기술
> 2. 모델 클래스의 필드(`models.XxxxxFeild`류)가 데이터베이스의 필드로 매핑됨
> 3. models.Model의 자식 클래스

1. 폼의 구조, 동작, 사용자에게 보여지는 방식들을 기술
2. 폼 클래스의 필드(`forms.XxxxxFeild`류)
   - `<input>`요소에 매핑됨
   - 클래스임
   - 폼 데이터를 저장하고 있음
   - 폼이 제출되면, 자신(필드)의 데이터(폼 데이터)에 대한 유효성 검사 실시
   - 폼의 필드는 웹 브라우저에서 위젯으로 표현됨
   - 필드 타입마다 디폴트 위젯 클래스가 있으며, 오버라이딩 가능
   - 위젯 클래스는 HTML `<input type>` 속성의 값으로 변환됨
3. 모든 폼 클래스는 django.forms.Form의 자식 클래스
4. 장고의 폼 클래스는 모든 필드에 대해 is_valid() 메소드를 갖고 있음
   - 메소드가 호출되면 유효성 검사를 실시하고
   - 모든 필드가 유효하다면
     - True를 반환
     - 폼 데이터를 clean_data 속성에 저장

### 장고에서 객체를 렌더링하는 세 가지 과정

1. 렌더링 할 객체를 뷰(View)로 가져오기 (예 : DB로부터 객체 추출함)
2. 그 객체를 템플릿(template) 시스템으로 넘겨주기
3. 템플릿 문법을 처리해서 HTML 마크업 언어로 변환하기 (즉, 템플릿 파일 생성됨 )

> 객체 : DB → View → Template → 변환

### 폼 객체

``` python
from django import forms

class ContactForm(forms.Form):
    subject = forms.CharFeild(max_length=100)
    message = forms.CharFeild(widget=forms.Textarea)
    sender = forms.EmailField()
    cc_myself = forms.BooleanField(required=False)
```

1. 폼도 객체이며 템플릿의 일부 : 템플릿 코드에 포함되어 렌더링 절차를 거치게 됨

2. 폼 객체에는 데이터가 없을 수도 있음을 유의 : 렌더링 이후 사용자가 데이터를 채우는 것이 보통

3. 언바운드 폼(Unbound Form) : 데이터 없이 만들어진 폼. 사용자에게 보여질 때 비어있거나 기본값으로 채워짐

4. 바운드 폼(Bound Form) : 데이터로 채우어진 폼. 제출된 데이터를 갖고 있고, 데이터의 유효성 검사에 사용

   데이터 채워서 폼 객체를 생성하는 방식

   - 저장된 모델 객체로부터 채우기

   - 직전에 제출된 HTML 폼으로부터 채우기

     > 폼 필드가 여러 개인데 한 필드에서 에러가 발생하여 폼 데이터를 재입력할 때, 에러가 없었던 필드들은 직전에 제출된 폼으로부터 데이터를 채우고 사용자에게 보여주는 방식으로 활용할 수 있음 (예 : 온라인쇼핑몰 주문서 작성 중 적립금 오류나도 사은품 고른 건 그대로인 상황)

5. 뷰에서 폼 객체를 생성 : 뷰에서 데이터 없이 만들지, 채워서 만들지 적절히 구분해서 코딩

6. HTML에서 `{{ form }}` 같은 템플릿 변수로 코딩함

   - 그 외, 개발자가 직접 템플릿에 넣어줘야 하는 것들

     : form 태그, submit 버튼, `{% csrf_token %}`, table 태그, ul 태그 등

### 렌더링 결과

```html
<p><label for="id_subject">Subject</label>
    <input id="id_subject" type="text" name="subject" maxlength="100" /></p>
<p><label for="id_message">Message</label>
    <input type="text" name="subject" id="id_message" /></p>
<p><label for="id_sender">Sender</label>
    <input type="email" name="sender" id="id_sender" /></p>
<p><label for="id_cc_myself">Cc myself</label>
    <input type="checkbox" name="cc_myself" id="id_cc_myself" /></p>
```

1. 레이블 텍스트
   - 디폴트 : 필드명의 첫 글자를 대문자로, 밑줄(_)을 빈칸( )으로 변경
     - 예 : 폼 클래스의 필드명 cc_myself → HTML 파일의 레이블 텍스트 Cc myself
   - 각 필드를 정의할 때 명시적으로 지정할 수 있음
2. `<input>`의 id 및 for 속성 값
   - "id_필드명" 으로 생성





-----------

> 추가 공부해야 하는 내용
>
> 1. Form 클래스를 views.py에 만든다는 뜻인가? 아님 forms.py 같은 별도 파일을 만들고, views.py에서 `from forms import ContactForm`하고, 뷰 함수/클래스에서 `form = ContactForm()` 이런 식으로 생성한다는 걸까? 후자겠지?
> 2. 그래서 레이블 텍스트를 명시적으로 지정하는 방법은?