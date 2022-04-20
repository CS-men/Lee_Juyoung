## 0421 FrontEnd

#### 1. 인터넷은 어떻게 동작하는가? (How does the internet work?)

두 개의 컴퓨터가 통신이 필요할 때, 우리는 다른 컴퓨터와 물리적으로 (보통 [이더넷 케이블](http://en.wikipedia.org/wiki/Ethernet_crossover_cable)) 또는 무선으로 (예를 들어, [WiFi](http://en.wikipedia.org/wiki/WiFi) 나 [Bluetooth](http://en.wikipedia.org/wiki/Bluetooth) 시스템) 연결되어야 합니다. 모든 현대 컴퓨터들은 이러한 연결 중 하나를 이용하여 연결을 지속할 수 있습니다.

![Two computers linked together](https://mdn.mozillademos.org/files/8441/internet-schema-1.png)

이러한 네트워크는 두 대의 컴퓨터로 제한되지 않습니다. 원하는 만큼의 컴퓨터를 연결할 수 있습니다. 그러나 이렇게 연결할 수록 매우 복잡해집니다. 예를 들어 10대의 컴퓨터를 연결하려는 경우 컴퓨터 당 9개의 플러그가 달린 45개의 케이블이 필요합니다!

![Ten computers all together](https://mdn.mozillademos.org/files/8443/internet-schema-2.png)

이 문제를 해결하기 위해 네트워크의 각 컴퓨터는 **라우터**라고하는 특수한 소형 컴퓨터에 연결됩니다. 이 라우터에는 단 하나의 작업만 있습니다. 철도역의 신호원처럼 주어진 컴퓨터에서 보낸 메시지가 올바른 대상 컴퓨터에 도착하는지 확인합니다. 컴퓨터 B에게 메시지를 보내려면 컴퓨터 A가 메시지를 라우터로 보내야하며, 라우터는 메시지를 컴퓨터 B로 전달하고 메시지가 컴퓨터 C로 배달되지 않도록해야합니다.

이 라우터를 시스템에 추가하면 10대의 컴퓨터 네트워크에는 10개의 케이블만 필요합니다. 각 컴퓨터마다 단일 플러그와 10개의 플러그가 있는 하나의 라우터가 필요합니다.

![Ten computers with a router](https://mdn.mozillademos.org/files/8445/internet-schema-3.png)

지금까지는 그런대로 잘되었습니다. 수백, 수천, 수십억 대의 컴퓨터를 연결하는 것은 어떨까요? 물론 단일 라우터는 그 정도까지 확장 할 수는 없지만 신중하게 읽으면 **라우터는 다른 컴퓨터와 마찬가지로 컴퓨터**라고 말했습니다. 그럼, 두 대의 라우터를 연결하지 못하게 하는 것이 있을까요? 없죠!

![Two routers linked together](https://mdn.mozillademos.org/files/8447/internet-schema-4.png)

컴퓨터를 라우터에 연결하고, 라우터에서 라우터로, 우리는 무한히 확장할 수 있습니다.

![Routers linked to routers](https://mdn.mozillademos.org/files/8449/internet-schema-5.png)





> 위성을 이용하면 신호가 위성까지 갔다가 다시 user에게 가기 때문에 많은 거리를 이동해야해서 비효율적이다.

> 도메인을 입력하면 -> DNS Server에 ip주소를 가져오기 위해 요청을 보내고 -> 브라우저가 다시 ip서버로 요청 보낸다.



---

#### 2. DNS는 어떻게 작동하는가? (DNS and how it works?) [Domain Name System]

서버에는 호스트라는것이 존재하는데 호스트에 대한 하나의 식별자를 호스트 네임이라고 부른다. [www.google.com ](http://www.google.com/) 이나 [www.pinterest.com ](http://www.pinterest.com/) 같은 웹사이트 주소를 호스트 네임이라고 부르며 DNS의 실질적 역할은 사용자가 입력한 호스트 네임을 해당 호스트에 해당하는 IP주소로 변환하는 것이다. 예를 들어 설명하자면 웹 브라우저에 주소 [www.youtube.com/video/15](http://www.google.com/index.html을) 를 입력했을때 DNS 프로토콜은 다음과 같은 순서로 동작된다.

1. 브라우저는 사용자가 입력한 주소로부터 호스트 네임(www.youtube.com)을 뽑아내고 이를 DNS 클라이언트 측에 넘긴다
2. DNS 클라이언트는 DNS 서버로 호스트 네임을 포함한 요청을 보낸다
3. DNS 클라이언트는 DNS 서버로부터 호스트 네임에 대한 IP 주소를 반환받는다
4. 브라우저가 DNS 클라이언트로부터 IP 주소를 전달받으면 해당 IP 주소의 80번 포트에 위치하는 HTTP서버로 TCP연결을 실행한다

DNS가 실질적으로 동작한 부분은 2번 -> 3번의 과정이다. 1번의 경우 브라우저에 [www.youtube.com](https://www.youtube.com/) 을 입력하면 로컬(브라우저를 사용하기 위해 이용중인 스마트폰이나 컴퓨터등의 장비) DNS 서버가 작동한다. 로컬 DNS 서버는 자주 이용하는 도메인을 캐시에 저장해놓고 있다가 저장중인 도메인으로 요청을 할 경우 DNS 클라이언트에 요청할 필요없이 바로 해당되는 IP 주소로 웹 페이지를 이동시킨다. 만약 캐시에 저장되어있지 않은 도메인일 경우 질의 방법이 두가지로 나누어지는데 크게 **반복적 질의**와 **재귀적 질의**로 나눠진다.

**반복적 질의**

![img](https://blog.kakaocdn.net/dn/buQjr1/btqRt6CqSg9/sazaxxqkMUvY92fjiT9tkk/img.png)



반복적 질의는 다음과 같은 순서로 동작된다.

1. 브라우저에서 로컬 DNS에 요청 -> 로컬이 DNS가 정보를 가지고 있지 않으면 루트 DNS에 요청
2. 루트 DNS는 자기는 모르지만 최상위 DNS는 알고 있을거라고 알려줌 -> 최상위 DNS에 요청
3. 최상위 DNS는 자기도 모르지만 책임 DNS는 알고 있을거라고 알려줌 -> 책임 DNS에 요청
4. 책임 DNS는 알고있기 때문에 해당 IP 주소를 반환함
5. 로컬 DNS는 전달받은 정보를 브라우저에 알려주고 자신의 DNS 레코드에 캐시형태로 해당 정보를 저장함(같은 요청에 대한 신속한 처리를 위함)

**재귀적 질의**

![img](https://blog.kakaocdn.net/dn/wLKmx/btqRGq7nO9B/J2TBFsW1tkNtAaAtVwLA5k/img.png)

재귀적 질의는 다음과 같은 순서로 동작된다.

1. 브라우저에서 로컬 DNS에 요청 -> 로컬이 정보를 가지고 있지 않으면 루트 DNS에 알고있냐고 물어봄
2. 루트 DNS는 모르기 때문에 최상위 DNS에 물어봄
3. 최상위 DNS도 모르게 때문에 책임 DNS에 물어봄
4. 책임 DNS는 알고있기 때문에 해당 IP주소를 반환함
5. 로컬 DNS는 전달받은 정보를 브라우저에 알려주고 자신의 DNS 레코드에 해당 정보를 저장함

이와같이 반복적 질의는 DNS 서버마다 로컬 DNS가 반복적으로 질문을 하는 방법이고 재귀적 질의는 각각의 DNS 서버가 상위 DNS 서버에 질문을 하는 방법이다. 그림을 보면 알수있다싶이 반복적 질의는 로컬 DNS가 모든 상위 DNS서버에 요청하는것에 반해 재귀적 질의는 요청을 받은 DNS 서버가 직접 다른 DNS 서버에 요청을 한다는 점에서 다르다. 요청의 주체가 다르다고 할 수 있을것이다.

> 처음에 youtube.com 이라고 입력한다 -> host file을 찾아보고 없으면 DNS Server에 요청한다. -> DNS Server에서 ip를 응답해 준다.
>
> 도메인 = Host Name 이다.

---

#### 3. Browsers and how they work?

1. DNS 에 호스트 ip 주소를 요청한다.

2. ip 주소를 받으면 Random Sequence (랜덤한 숫자가 적힌 번호표) 를 가지고 서버에 간다

3. 브라우저가 Random Sequence를 서버에게 주고, 서버는 다시 번호표에 +1 을 해서 브라우저에게 준다.

4. 그리고 다시 브라우저는 +1을 해서 서버에게 준다. => 3 Way-Handshake

5. 서버에게 데이터를 요청한다. => HTTP Request

6. 서버는 데이터를 응답한다. => HTTP Response

7. 브라우저는 받은 데이터를  W3C의 명세에 따라 HTML 과 CSS를 해석한다. => Parsing

8. 브라우저의 렌더링 엔진은 HTML을 Parsing 하여 DOM Tree를 생성한다.

9. 이 때 렌더링 엔진이 스타일 태그를 만나면 HTML Parsing을 중단하고 CSS Parsing을 시작하고 CSSOM Tree를 만든다.

10. CSS Parsing이 끝나면 다시 HTML Parsing을 시작한다.

11. 그러다가 스크립트<Script> 태그를 만나면 다시 Parsing을 중단하고 JS Engine에게 권한을 넘기고 추상 구문 트리인 AST(Abstract Syntax Tree)를 만들고 실행한다.

12. 다시 HTML Parsing을 마무리 하고 DOM Tree 와 CSSOM Tree 를 합쳐서 Render Tree를 생성한다.

13. 여기까지 과정을 **Construction** 이라고 한다.

14. 렌더링 엔진은 Layout 작업을 시작한다. (Render Tree의 노드들을 화면의 올바른 위치에 표시한다.)

15. UI Backend가 Render Tree의 노드들을 돌면서 UI를 그린다.

16. 노드들의 레이어를 순서대로 구성하는 Composition 단계를 시작한다. (z-index가 낮은 요소부터 높은 요소 순으로 놓는다.)

17. Layout 작업부터 Composition 까지의 과정을 **Operation** 이라고 한다.



> 데이터를 다 받고 시작하는게 아니라 일부 데이터를 받으면 화면에 표시하고, 또 데이터를 받고 화면에 표시하는 걸 반복한다. (유저에게 빠르게 화면을 표시해주기 위해서)



#### (참고)브라우저의 기본 구조

브라우저의 주요 구성 요소는 다음과 같다.(1.1)

1. 사용자 인터페이스 - 주소 표시줄, 이전/다음 버튼, 북마크 메뉴 등. 요청한 페이지를 보여주는 창을 제외한 나머지 모든 부분이다.
2. 브라우저 엔진 - 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어.
3. 렌더링 엔진 - 요청한 콘텐츠를 표시. 예를 들어 HTML을 요청하면 HTML과 CSS를 파싱하여 화면에 표시함.
4. 통신 - HTTP 요청과 같은 네트워크 호출에 사용됨. 이것은 플랫폼 독립적인 인터페이스이고 각 플랫폼 하부에서 실행됨.
5. UI 백엔드 - 콤보 박스와 창 같은 기본적인 장치를 그림. 플랫폼에서 명시하지 않은 일반적인 인터페이스로서, OS 사용자 인터페이스 체계를 사용.
6. 자바스크립트 해석기 - 자바스크립트 코드를 해석하고 실행.
7. 자료 저장소 - 이 부분은 자료를 저장하는 계층이다. 쿠키를 저장하는 것과 같이 모든 종류의 자원을 하드 디스크에 저장할 필요가 있다. HTML5 명세에는 브라우저가 지원하는 '[웹](http://www.html5rocks.com/en/features/storage)[ ](http://www.html5rocks.com/en/features/storage)[데이터](http://www.html5rocks.com/en/features/storage)[ ](http://www.html5rocks.com/en/features/storage)[베이스](http://www.html5rocks.com/en/features/storage)'가 정의되어 있다.

![brouser1](https://d2.naver.com/content/images/2015/06/helloworld-59361-1.png)

그림 1 브라우저의 주요 구성 요소

크롬은 대부분의 브라우저와 달리 각 탭마다 별도의 렌더링 엔진 인스턴스를 유지하는 것이 주목할만하다. 각 탭은 독립된 프로세스로 처리된다.

https://d2.naver.com/helloworld/59361

---

### 4. What is hosting?

호스팅(hosting)이란 그 단어 뜻에서도 느껴지듯이 대형 서버의 기능을 빌려쓰는 것을 의미합니다.

전문 호스팅사의 서버를 빌려 그 안에 나만의 공간을 빌리는 것을 호스팅이라고합니다.

호스팅사마다 호스팅종류는 다양하지만 크게 웹호스팅, 서버호스팅, 클라우드호스팅으로 구분할 수 있습니다.

  **웹호스팅**은 하나의 서버장비를 여러명이 공유하여 사용하는 것입니다. 따라서 가격도 저렴하고 대중적으로 
가장 많이 사용되는 호스팅입니다. 기업이나 개인 홈페이지는 웹트래픽양이 많지 않기 때문에 웹호스팅을 
사용하는 것이 가장 적합합니다. 하지만 트래픽양이 증가해서 혼자 너무 많은 트래픽을 잡아먹는다면 
서버가 다운되는 등의 제약이 있을 수 있습니다.

 **서버호스팅**은 웹호스팅과 반대로 한명의 고객이 하나의 서버장비를 임대하는 호스팅입니다. 따라서 가격도 비싸고 스케일과 트래픽양이 많은 대형홈페이지를 구축할 때 사용하는 서비스입니다. 서버를 단독사용하므로 설치, 삭제등의 개발이 자유롭다고 합니다. 고정적으로 트래픽양이 많은 사이트에 적합한 호스팅입니다.

 **클라우드호스팅**은 서버호스팅과 비슷하지만 물리적서버장비가아닌 가상서버를 임대한다는 데 차이가 있습니다. 따라서 자유롭게 서버스펙을 조절할 수 있고, 이용한 만큼만 금액을 지불하면 된다는 장점이 있습니다. 일시적인 트래픽 변동량이 많은 사이트에 적합한 호스팅입니다.

> 서버를 빌린다는 것은 같지만 용도에 따라서 웹, 서버, 클라우드호스팅을 선택하면 된다.

---

### 5. What is Domain Name?

#### IP란?

인터넷에 연결되어 있는 장치(컴퓨터, 스마트폰, 타블릿, 서버 등등)들은 각각의 장치를 식별할 수 있는 주소를 가지고 있는데 이를 ip라고 한다. 예) 115.68.24.88, 192.168.0.1

#### 도메인(domain)이란?

ip는 사람이 이해하고 기억하기 어렵기 때문에 이를 위해서 각 ip에 이름을 부여할 수 있게 했는데, 이것을 도메인이라고 한다.

- opentutorials.org -> 115.68.24.88
- naver.com -> 220.95.233.172
- daum.net -> 114.108.157.19

![img](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/121/298.png)

#### (참고)도메인의 구성요소

컴퓨터의 이름과 최상위 도메인으로 구성되어 있다. 예를들면 아래와 같다.

- opentutorials.org
  - opentutorials : 컴퓨터의 이름
  - org : 최상위 도메인 - 비영리단체
- daum.co.kr
  - daum : 컴퓨터의 이름
  - co : 국가 형태의 최상위 도메인을 의미
  - kr : 대한민국의 NIC에서 관리하는 도메인을 의미

> 위에서 설명했듯이 ip를 사람들이 쉽게 기억하기 위해 만든 이름이다.
>
> DNS Server를 이용해서 ip 주소를 찾을 수 있다.
