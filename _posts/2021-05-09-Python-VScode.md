---
layout: single
title:  "[Python][VScode][오류][해결] 용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오."

---

### 오류 내용

VScode 에서 .py 파일을 실행하려던 중, 터미널에 빨간 색으로 **'용어가 cmdlet, 함수, 스크립트 파일 또는 실행할 수 있는 프로그램 이름으로 인식되지 않습니다. 이름이 정확한지 확인하고 경로가 포함된 경우 경로가 올바른지 검증한 다음 다시 시도하십시오. ...'** 와 같은 오류 메세지가 떴다.



### 해결과정

1. [구글링하니 python 설치 경로가 잘못 지정된 것이 원인이라고 함](https://sun-kakao.tistory.com/92)
2. 환경변수를 확인하니 정말 파이썬 설치 경로가 없었음
3. 설치 경로를 확인을 위해 명령 프롬프트에 where python을 쳤더니 경로가 2개가 나옴
   <img src="C:\Users\USER\Documents\Develop\dev-iwin.github.io\assets\images\210509-two-pathes.png" alt="two pathes" style="zoom:80%;"/>
4. [윈10의 '앱 실행 별칭 관리'에서 python 관련 항목을 모두 끄면 꼬인 경로가 해결됨](https://my-repo.tistory.com/19)
   <img src="C:\Users\USER\Documents\Develop\dev-iwin.github.io\assets\images\MAEA.png" alt="Manage App Execution Aliases" style="zoom:50%;" />
   <img src="C:\Users\USER\Documents\Develop\dev-iwin.github.io\assets\images\210509-clean-path.png" alt="clean path" style="zoom:80%;" />
5. 그런데 여전히 VS code 터미널의 오류 메세지가 떴음
6. [VS code 의 기본 터미널 종류가 power shell 로 되어 있어서 오류가 난다고 함](https://somjang.tistory.com/entry/Windows-Visual-Studio-Code-%EC%9D%B4-%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%97%90%EC%84%9C-%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%A5%BC-%EC%8B%A4%ED%96%89%ED%95%A0-%EC%88%98-%EC%97%86%EC%9C%BC%EB%AF%80%EB%A1%9C-%ED%95%B4%EA%B2%B0%EB%B0%A9%EB%B2%95)
7. Terminal: Select Default Profile 을 cmd로 변경하여 해결함(Git Bash도 된다고 함)



### 그리고 남은 의문

그러면, power shell을 기본으로 쓸 수 없는 건가?