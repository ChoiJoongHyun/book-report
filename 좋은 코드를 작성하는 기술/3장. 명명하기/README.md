3장. 명명하기
-------------

### 좋은 코드는 좋은 이름에서 나온다

> 좋은 명칭을 사용하는 것이 왜 필요한가? 좋은 명칭을 사용하게 되면 읽기 쉽고 이해하기 쉬운 코드가 된다. 이말은 유지보수성 또한 향상된다는 뜻이다.

### 좋은 이름의 조건

###### - 설명적이고 의미, 의도를 나타내야 한다.

> 좋은 번수명, 메소드명, 클래스명은 이름이 그 내용을 올바르게 나타낸다. 그러한 이름은 코멘트를 읽을 필요도 없이 이름을 보는 것만으로도 그 역할을 이해 할 수 있다.
>
> -	소비세를 콤마 방식의 금액표시로 문자열 변환
>
> ```
> String s = fmt(value);
> ```
>
> 변수명 (s, value) 와 메소드명 (fmt)가 매우 짧아 이름만 봐서 무슨 역할인지 알 수 없다.
>
> ```
> String formattedConsumptionTax = insertGroupingSeparators(consumptionTax);
> ```
>
> 변수명과 메소드명이 모두 매우 길어 이름이 해당 역할을 설명하고 있으므로 코멘트가 없어도 이해하기 쉬우나 이름이 너무 길면 반대로 코드의 가독성이 떨어진다.
>
> ```
> String formattedTax = insertGroupSeps(consumptionTax);
> ```
>
> 변수명과 메소드명을 조금 생략하였다. 다만 생략에 의해서 오히려 의미가 난해하게 되는것에 중의해라.
>
> -	생략의 요령
> 	-	선두 몇개의 문자만을 남긴다. 또한 복수형인 경우는 마지막에 s를 남긴다.
> 		-	Separators -> Seps
> 	-	ing 의 삭제
> 		-	Grouping -> Group
> 	-	단어의 삭제
> 		-	formattedConsumptionTax -> formattedTax
> 	-	어두 이외의 모음을 삭제한다.
> 		-	image -> img
> 	-	강한 음을 남긴다.
> 		-	server -> svr
> 	-	일반적인 약어를 이용한다.
> 		-	database -> db

###### - 일관성이 있어야 한다.

> 좋은 이름은 코드 전체를 통해 일관된 정책으로 명명된다.
>
> -	대칭성이 유지되어야 한다.
> 	-	begin/end, write/read, on/off 등
> -	단어의 조합 방식이 일관되어야 한다.
> 	-	scoreAvg, scoreAverage, avgScore 등을 혼재해서 사용하지 않는다.

###### - 영어로 부여되어야 한다.

> -	존재하지도 않는 단어로 명명하지 않기
> 	-	많이 틀리는 단어로는 regist 이다. 이 단어는 존재하지 않는다. register 이다.
> -	스펠링을 틀리지 않도록 하기
> -	오역에 주의하기

###### - 관용표현을 따르고 있어야 한다.

> 언어마다, 대상 영역마다, 회사나 팀마다 명명에 관한 관용표현(또는 룰) 이 있다.

###### - 코딩 표준을 따라야 한다.

### 변수명

> 변수명은 소스 코드 내의 여러 곳에서 선언, 대입, 참조의 형식으로 몇 번이고 등장한다. 자주 등장하는 만큼 좋은 변수명이 부여된다면 코드의 가독성은 상당히 높아지게 된다.

###### - 기본은 설명적인 이름으로 시작한다.

> 변수명을 보는 것만으로도 무엇이 어떠한 역할을 위해 대입되고 있는지 명확히 알 수 있다면, 좋은 이름이라고 할 수 있다.
>
> -	잘못된 표현의 예
>
> ```java
> //무슨 수치?
> int n;
> //무슨 언어?
> String[] language = {"ko", "en"};
> //무슨 플래그?
> boolean flg = false;
> //무슨 유저 에이전트?
> UserAgent userAgent;
> ```
>
> -	올바른 표현의 예
>
> ```java
> //주문수량
> int orderCount;
> //이용 가능한 언어
> String[] availableLanguage = {"ko", "en"};
> //동성명이 존재하는가?
> boolean existSameName = false;
> //알수없는 유저 에이전트
> UserAgent unknownUserAgent;
> ```

###### - 글로벌 변수, 클래스 변수, 필드 변수 (의미를 바르게 표현하기)

> 글로벌 변수, 클래스 변수, 필드 변수는 로컬 변수에 비해 변수의 스코프가 넓으므로 해당 변수의 의미를 올바르게 표현한 이름을 사용하는 것이 바람직하다.

###### - 로컬 변수 (스코프의 길이에 따라 사용을 구분하기)

> -	관용표현을 따른다/따르지 않는다.
>
> ```java
> // X 루프 카운터의 변수명이 관용적 표현이 아니라 너무 길다.
> for(int empCounter = 0; empCounter < employes.size; empCounter ++) {
>     Employee emp = employes[empCounter];
> }
>
> // O 루프 카운터의 이름이 짧은 관용적 표현으로 가독성이 높다.
> for(int i = 0; i < employes.size; i ++) {
>     Employee emp = employes[i];
> }
>
> // O 좌표계는 x, y 를 사용하는게 가독성이 높다.
> for(int x = 0; x < width; x ++) {
>     for(int y = 0; y < height; y ++) {
>     }
> }
> ```

###### - 메소드의 파라미터 (알기 쉽게 간결히)

> ```java
> // X account 의 의미가 불분명
> public void updateItem(Item item, Account account)
> // O account 는 갱신자의 정보인 것이 명확함
> public void updateItem(Item item, Account updater)
> ```

### 메소드명

> 좋은 메소드명은 이름으로부터 그 기능을 상상할 수 있어야 한다. 메소드명은 '동사' + '목적어' 로 되어 있는 경우가 많다.
>
> -	값 취득에 관한 메소드 : getXXX
> -	값 설정에 관한 메소드 : setXXX
> -	생성에 관한 메소드 : create, build, make, generate
> -	초기화에 관한 메소드 : initialize, setUpXXX
> -	파기 처리에 관한 메소드 : destroy, dispose
> -	상태 확인에 관한 메소드 : contain, exists
>
> 인스턴스 메소드는 'dateFormat.parse' 와 같이 객체명과 조합되어 호출되므로 조합되었을 때에 중복됨이 없이 의미가 통하는 이름이면 좋다. 물론 클래스 메소드와 클래스명도 동일하다. 자주 사용되는 메소드는 간결하고 짧은 이름을 사용하는 것이 좋다고 한다.

### 클래스명

> 변수명이나 메소드명에 비해 클래스명은 사이즈가 크므로 적절하고 좋은 클래스 명을 붙이는 것은 특히 중요하다.
>
> 클래스명이 잘 떠오르지 않을 때에는 자신이 만들려고 하는 클래스의 역할을 확실하게 정리하지 못한 게 아닌가 의심해 보아야 한다.
>
> 한 개의 클래스에 복수의 역할과 책임이 있는가?, 역할이 애매하지는 않은가?, 이러한 경우 해결하고자 하는 문제를 차분히 생각하여 클래스를 재설계할 필요가 있다.
>
> **'클래스의 이름 명명' = '설계' 인 셈이다.**
>
> > *클래스의 이름 명명이 곧 설계이다.. 공감이 가는 글이다. 클래스의 이름이 명확히 떠오르지 않을 때에는 구조를 다시 한번 생각해 보아야 겠다.*

###### - 클래스명의 어휘는 경험과 함께 향상된다

> 숙련도별 자주 이용되는 클래스명
>
> -	프레임워크 제작자가 이용하는 레벨의 클래스명 [프레임워크/라이브러리 개발]
> 	-	\*Scope, \*Loader, \*Engine, \*Provider, \*Conversion, \*Bhaviour, \*Descriptor, \*Cache, \*Resolver, \*Processor
> -	프레임워크를 확장한 클래스에서 사용하는 레벨의 클래스명
> 	-	\*Listener, \*Handler, \*Runner, \*Command, \*Observer, \*Node, \*Adaptor, \*Proxy, \*Holder, \*Context, \*Monitor, \*State\*, Builder, \*Factory, \*Visitor, \*Decorator, \*Strategy
> -	업무 웹 애플리케이션 개발 클래스명
> 	-	\*Action, \*Controller, \*Dto, \*Logic, \*Service, \*Util, \*Entity, \*Helper, \*Support, \*Dao, \*Manager, \*Bean, \*Form, \*Exception, \*Validator, \*Test, \*Impl

### 패키지/네임스페이스명

> 클래스나 리소스의 논리적인 그룹핑을 행하여 계층구조를 형성한다. 이것은 주로 이름의 충돌을 막기 위해서 사용된다.
>
> 패키지명은 그룹의 논리적인 내용을 나타내는 간결한 명사로 선택한다.

### 프로젝트명

> 프로젝트명을 기초로 패키지명, 데이터베이스의 스키마명, git 이나 svn 의 repository 명이 정해진다. 처음에 대충 프로젝트명을 붙이면 나중에 변경할 때 꽤 고생한다.

### 정리

> *개발을 하다 보면 클래스명, 메소드명, 변수명.. 을 생각해 내는 시간이 굉장히 많이 소요되는 것이 느껴진다.. 코드 리딩, 코드 리뷰를 통해 여러가지 네이밍에 대해 많이 알아놔야 겠다.*
