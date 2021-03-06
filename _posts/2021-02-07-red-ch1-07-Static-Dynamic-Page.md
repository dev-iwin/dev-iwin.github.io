---
layout: single
title:  "웹 프로그래밍의 이해 07 - 정적 페이지와 동적 페이지"

---

*책 <Django로 배우는 쉽고 빠른 웹 개발, 파이썬 웹 프로그래밍> 1단원 내용을 복습 겸 정리하며...*

## 정적(static) 페이지

* 누가, 언제 요구하더라도 항상 같은 내용을 표시하는 웹 페이지
* 해당 웹 서비스의 제공자가 사전에 준비하여 서버 측에 배치한 것
* 동일한 리소스(URL)의 요청에 대해서는 항상 동일한 내용의 페이지를 반환
* 주로, HTML, 자바스크립트, CSS, 이미지만으로 이루어진 페이지
* 초창기 웹 출현 당시, 정적인 웹 페이지들을 하이퍼링크로 연결하여 보여주는 것이 웹 서버의 주된 역할

## 동적(dynamic) 페이지

* 누가, 언제 요구하는지에 따라 각각 다른 내용이 반환되는 페이지
* 동적 페이지에는 프로그래밍 코드가 포험되어 있어 페이지 요청 시점에 HTML 문장을 만들어 냄
* 예 : 현재 시각을 보여주는 페이지, (사용자마다 다른 물건, 개수를 담는) 온라인 쇼핑몰의 장바구니 페이지
* 점차, 동적 페이지와 데이터베이스 처리 등에 대한 요구사항이 증가함에 따라 웹 서버와는 다른 별도의 프로그램이 필요하게 됨

## CGI(Common Gateway Interface) 규격

* 웹 서버와 별도의 프로그램 사이에 정보를 주고 받는 규칙을 정의한 것



