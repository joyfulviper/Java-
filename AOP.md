## AOP<br>
* Weaving: PointCut으로 결정된 타겟에 부가기능을 삽입하는 과정<br>

## Weaving의 종류<br>
* 컴파일 타임 위빙<br>
AspectJ라는 특수한 컴파일러가 Aspect코드와 Base코드를 입력받아 Weaving클래스를 생성한다.
* 런타임 위빙<br>
실제 런타임상에서 method 호출시 위빙이 이루어지는 것이다. (Source file, class 파일에도 변화가 없다.) 
타겟 클래스의 프록시를 생성하여 비즈니스 코드와 Advice가 포함된 메소드를 호출하는 방식이다. 실제 Spring AOP 에서 이 방식을 사용하고 있다.
* 로드타임 위빙<br>
클래스가 JVM에 로드되는 시점에때 advice가 위빙이 되는 것을 말한다.
LoadTimeWeaver라는 위빙을 해주면 이는 spring-instrument 의존성에 포함되어있다.

## JDK Proxy와 CGLib Proxy<br>
Spring에서는 자동으로 Target의 프록시 객체를 생성해 주는데, JDK Proxy(Dynamic Proxy)와 CGLib Proxy를 만들 수 있다.<br>
두 방식의 가장 큰 차이점은 Target의 어떤 부분을 상속 받아서 프록시를 구현하느냐에 있다.<br>
* JDK Proxy<br>
상위 인터페이스를 상속 받아 프록시를 만든다. 따라서 인터페이스를 구현한 클래스가 아니면 의존할 수 없다.
Target에서 다른 구체 클래스에 의존하고 있다면, JDK 방식에서는 그 클래스(빈)를 찾을 수 없어 런타임 에러가 발생한다.
* CGLib Proxy<br>
클래스를 상속 받아 프록시를 만든다.JDK 방식과는 달리 인터페이스를 구현하지 않아도 되고, 구체 클래스에 의존하기 때문에 런타임 에러가 발생할 확률도 상대적으로 적다. 또한 JDK Proxy는 내부적으로 Reflection을 사용해서 추가적인 비용이 들지만, CGLib는 그렇지 않다고 한다. 여러 성능 상 이점으로 인해 Spring Boot에서는 CGLib를 사용한 방식을 기본으로 채택하고 있다

## @Transactional<br>
트랜잭션 처리를 위한 @Transactional 애노테이션은 Spring AOP의 대표적인 예이다. 
@Transactional 또한 Proxy 형태로 동작한다.<br>
1. target에 대한 호출이 들어오면 AOP proxy가 이를 가로채서(intercept) 가져온다.<br>
2. AOP proxy에서 Transaction Advisor가 commit 또는 rollback 등의 트랜잭션 처리를 한다.<br>
3. 트랜잭션 처리 외에 다른 부가 기능이 있을 경우 해당 Custom Advisor에서 그 처리를 한다.<br>
4. 각 Advisor에서 부가 기능 처리를 마치면 Target Method를 수행한다.<br>
5. interceptor chain을 따라 caller에게 결과를 다시 전달한다.<br>

* @Transactional 적용 예제<br>
private는 트랜잭션 처리를 할 수없다. (프록시 객체는 인터페이스 또는 타겟 객체를 상속 받아서 구현하기 때문)<br>

