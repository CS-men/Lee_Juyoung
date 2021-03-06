## 04.13 토스 CS 면접 준비 (FrontEnd)

### 1. 브라우저 렌더링 원리

   - **홈페이지가 사용자에게 보이는 순서에 대해서 설명하시오.**

   ##### 동작 과정

   렌더링 엔진은 통신으로부터 요청한 문서의 내용을 얻는 것으로 시작하는데 문서의 내용은 보통 8KB 단위로 전송된다.

   다음은 렌더링 엔진의 기본적인 동작 과정이다.

   ![brouser2](https://d2.naver.com/content/images/2015/06/helloworld-59361-2.png)

   그림 2 렌더링 엔진의 동작 과정

   렌더링 엔진은 HTML 문서를 파싱하고 "콘텐츠 트리" 내부에서 태그를 [DOM](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/) 노드로 변환한다. 그 다음 외부 CSS 파일과 함께 포함된 스타일 요소도 파싱한다. 스타일 정보와 HTML 표시 규칙은 "[렌더](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)[ ](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)[트리](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)"라고 부르는 또 다른 트리를 생성한다.

   렌더 트리는 색상 또는 면적과 같은 시각적 속성이 있는 사각형을 포함하고 있는데 정해진 순서대로 화면에 표시된다.

   렌더 트리 생성이 끝나면 배치가 시작되는데 이것은 각 노드가 화면의 정확한 위치에 표시되는 것을 의미한다. 다음은 UI 백엔드에서 렌더 트리의 각 노드를 가로지르며 형상을 만들어 내는 그리기 과정이다.

   일련의 과정들이 점진적으로 진행된다는 것을 아는 것이 중요하다. 렌더링 엔진은 좀 더 나은 사용자 경험을 위해 가능하면 빠르게 내용을 표시하는데 모든 HTML을 파싱할 때까지 기다리지 않고 배치와 그리기 과정을 시작한다. 네트워크로부터 나머지 내용이 전송되기를 기다리는 동시에 받은 내용의 일부를 먼저 화면에 표시하는 것이다.

   ##### 동작 과정 예

   ![brouser3](https://d2.naver.com/content/images/2015/06/helloworld-59361-3.png)

   그림 3 웹킷 동작 과정

    ![brouser4](https://d2.naver.com/content/images/2015/06/helloworld-59361-4.png)

   그림 4 모질라의 게코 렌더링 엔진 동작 과정(3.6)

   웹킷과 게코가 용어를 약간 다르게 사용하고 있지만 동작 과정은 기본적으로 동일하다는 것을 그림 3과 그림 4에서 알 수 있다.

https://d2.naver.com/helloworld/59361

---

### 2. 호이스팅에 대해서 설명해 보시오.

**호이스팅(Hoisting)의 개념**
함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것을 말한다.

**호이스팅이란**
자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모두 모아서 유효 범위의 최상단에 선언한다.
자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑는다.
함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킨다.
유효 범위: 함수 블록 {} 안에서 유효
즉, 함수 내에서 아래쪽에 존재하는 내용 중 필요한 값들을 끌어올리는 것이다.
실제로 코드가 끌어올려지는 건 아니며, 자바스크립트 Parser 내부적으로 끌어올려서 처리하는 것이다.
실제 메모리에서는 변화가 없다.
https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html

> 트위치 호스팅(hosting) 이랑 같은 개념인지 찾아봤는데 스펠링도 다르고 다른 개념인듯 비슷한 개념인듯 다른개념이다.

---

### 3. 클로저는 무엇인가요? 원리와 왜 사용하는지 설명하시오.

클로저는 독립적인 (자유) 변수를 가리키는 함수이다. 클로저 안에 정의된 함수는 만들어진 환경을 '기억한다'.

**클로저를 통한 은닉화**

일반적으로 JavaScript에서 객체지향 프로그래밍을 말한다면 Prototype을 통해 객체를 다루는 것을 말한다. Prototype을 통한 객체를 만들 때의 주요한 문제 중 하나는 Private variables에 대한 접근 권한 문제이다. 특별한 인터페이스를 제공하는 것이 아니라면, 여기서는 외부에서 접근할 방법이 전혀 없다.

**클로저의 성능**

클로저는 각자의 환경을 가진다. 이 환경을 기억하기 위해서는 당연히 메모리가 소모될 것이다. 클로저를 생성해놓고 참조를 제거하지 않는 것은 C++에서 동적할당으로 객체를 생성해놓고 `delete`를 사용하지 않는 것과 비슷하다. 클로저를 통해 내부 변수를 참조하는 동안에는 내부 변수가 차지하는 메모리를 GC가 회수하지 않는다. 따라서 클로저 사용이 끝나면 참조를 제거하는 것이 좋다.

이처럼 메모리 관리에 있어서 약점이 있찌만 추가로 스코프 체인을 검색하는 시간과 새로운 스코프를 생성하는데 드는 비용도 감안하지 않을 수 없다.

https://hyunseob.github.io/2016/08/30/javascript-closure/

---

### 4. 브라우저 저장소에 대해서 차이점을 설명하시오. 

## Web Storage의 차이점(cookie와 비교)

- 쿠키는 매번 서버로 전송된다.

웹 사이트에서 쿠키를 설정하면 이후 모든 웹 요청은 쿠키정보를 포함하여 서버로 전송된다. Web Storage는 저장된 데이터가 클라이언트에 존재할 뿐 서버로 전송은 이루어지지 않는다. 이는 네트워크 트래픽 비용을 줄여 준다.

- 단순 문자열을 넘어(스크립트) 객체정보를 저장할 수 있다.

문자열 기반 데이터 이외에 체계적으로 구조화된 객체를 저장할 수 있다는 것은 개발 편의성을 제공해주는 주요한 장점이 된다. 브라우저의 지원 여부를 확인해 봐야 하는 항목이다.

- 용량의 제한이 없다

쿠키는 개수와 용량에 있어 제한이 있다. 하나의 사이트에서 저장할 수 있는 최대 쿠키 수는 20개이다. 그리고 하나의 사이트에서 저장할 수 있는 최대 쿠키 크기는 4KB로 제한되어 있다. 그러나 Web Storage에는 이러한 제한이 없다. 그러나 쿠키도 하위키를 이용하면 이러한 제한을 일부 해소할 수 있습니다. 그리고 대부분 쿠키의 제한으로까지 데이터를 저장할 일이 없다.

- 영구 데이터 저장이 가능하다

쿠키는 만료일자를 지정하게 되어 있어 언젠가 제거된다. 만료일자로 지정된 날짜에 쿠키는 제거되는 것이다. 만약 만료일자를 지정하지 않으면 세션 쿠키가 된다. 만일 영구 쿠키를 원한다면 만료일자를 굉장히 멀게 설정하여 해결할 수 있다.
WebStorage는 만료기간의 설정이 없다. 즉, 한번 저장한 데이터는 영구적으로 존재하는 것이다.

WebStorage와 쿠키의 차이점에 대해서 WebStorage가 특별히 좋은 이유는 없다고 봐도 무방하다. 다만 한가지 매번 서버로 전송되지 않는다는 특징은 꽤나 유용하다.

https://velog.io/@ejchaid/localstorage-sessionstorage-cookie%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90

---

### 5. JavaScript는 어떤 언어인가요?

-> 싱글 스레드 언어

---



FE 정리 잘해둠

https://realmojo.tistory.com/300



