---
layout: single
title:  "CSS3의 Color와 Background"

---

## 색상 표현

1. 16진수 표기법
   - 기호 # 다음에 6자리의 16진수(0~f)
   - 앞에서부터 두자리씩 묶어 R, G, B를 의미 : #RRGGBB
   - 검정(#000000) ~ 하양(#ffffff)
   - 두자리씩 중복될 경우 줄여서 표기 가능 : #ffff00 → #ff0
   - `#00ff00`
2. rgb와 rgba
   - rgb, rgba 함수에 십진수로 표현
   - R, G, B는 0~255 (0 안 섞임, 255 가득 섞임)
   - 투명도 a는 0~1 (소수점 앞 0 생략 가능)
   - `rgba(0, 255, 0, .5)`
3. hsl과 hsla
   - hsl, hsla 함수에 색상(hue), 채도(saturation), 명암(lightness) 값을 기입
   - 색상(hue) : 색상환의 각도를 0~360으로 표현 (R 0, G 120, B 240)
   - 채도(saturation) : 색의 선명함으로 0~100%로 표현 (100%가 순색)
   - 명암(lightness) : 밝고 어두운 정도로 0~100%로 표현(100%가 가장 밝음)
   - 투명도 a는 0~1 (소수점 앞 0 생략 가능)
   - `hsla(120, 100%, 100%, 0.5)`
4. 색상 이름 표기법
   - 모든 브라우저에서 표현 가능한 웹 안전 색상 216개 (기본 색상 16개 포함)
   - `green`

## 배경 관련 속성 및 값

1. background-color

2. background-clip : 배경 적용 범위

   - border-box : 기본값
   - padding-box
   - content-box

3. background-image

   - `url("파일 경로")`

4. background-repeat : 배경 이미지 반복 방법

   - repeat : 기본값
   - repeat-x : 가로 반복
   - repeat-y : 세로 반복
   - no-repeat

5. background-size : 배경 이미지 크기 조절

   - auto : 원본 크기, 기본값
   - contain : 요소 안에 배경 이미지가 다 들어오도록 확대/축소 (요소 내 여백이 생길 가능성이 있음, 이미지 비율 유지됨)
   - cover : 배경 이미지로 요소를 모두 덮도록 이미지를 확대/축소 (요소 내 여백 없음, 이미지 비율 변경될 가능성 있음)
   - 크기값 : 너비 값, 높이 값. 너비 값만 지정하면 높이는 기존 비율에 맞게 자동 조정
   - 백분율 : 요소의 크기를 기준으로 백분율 값을 지정하고 그에 맞춰 이미지 확대/축소

6. background-position : 배경 이미지 위치 조절

   - 수평 위치 : left | center | right | 길이 값 | 백분율
   - 수직 위치 : top | center(기본값) | bottom | 길이 값 | 백분율
   - 값을 하나만 입력시 수평 위치를 지정한 것으로 인식

7. background-origin : 배경 이미지 배치 기준

   - border-box
   - padding-box : 기본값
   - content-box

8. background-attachment : 배경 이미지 고정 여부

   - scroll : 기본값
   - fixed

9. background

   | 번호 | 속성(실제로 안 씀)    | 속성 값(이것만 씀)                                |
   | ---- | --------------------- | ------------------------------------------------- |
   | 3    | background-image      | `url("파일 경로")`                                |
   | 4    | background-repeat     | repeat \| repeat-x \| repeat-y \| no-repeat       |
   | 8    | background-attachment | scroll \| fixed                                   |
   | 6    | background-position   | <수평 위치> <수직 위치>                           |
   | 2    | background-clip       | border-box \| padding-box \| content-box          |
   | 7    | background-origin     | border-box \| padding-box \| content-box          |
   | 5    | background-size       | auto \| contain \| cover \| <크기 값> \| <백분율> |



_______

*보통 background-clip이랑 background-origin 중에 하나만 쓰게 되나? 9번 background 속성으로 입력할 때는, 속성 값들의 순서가 중요한가?*