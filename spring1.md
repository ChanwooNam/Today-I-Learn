# spring  

### applictionContext

- 분리해서 각자 필요한 아이를 import 해서 쓸 수 있다. 

  ```
  <beans>
  	<import resouce="context-dsafdsaf.xml"/>
      <import resouce="context-123456.xml"/>
  </beans>
  ```

- 등록된 객체는 미리 다 메모리에 올라간다. 옵션으로 그 시점을 늦추는 것도 가능하다.

- lazy-init="true"를 통해서 늦추고 불러오고 싶은 순간에 불러오면 된다. 

  ```
  -applicationContext.xml-
  <bean id="samsung" class="spring.tv.SamsungTV" lazy-init="true"/>
  -TVuser.java-
  Tv user = (Tv) applicationContext.getBean("samsung");
  // applicationContext(spring)야 너가 관리하는 애중에 samsung이라 하는 bean 하나 줘
  // singletone 이면 samsung을 다시 불러도 reuse 해서 사용할 것임 
  ```

- 아래와 같이 마킹해서 불러오는 것도 가능하다. 

  ```
  Tv user2 = applicationContext.getBean("lg", Tv.class);
  ```

- singletone 설정도 가능하다. 

  ```
  <bean id="lg" class="spring.tv.LgTV" lazy-init="true" scope="singleton"/>
  
  scope="singleton" , scope="prototype"
  
  System.out.println("singletone ?"+(user==user2));
  ```

  scope="prototype" 으로 설정하면  false로 결과가 나오는 것을 볼 수 있다. 그러면 요청이 들어올때 마다 계속 찍어낼 것이다. 

### Factory method 

생성자로 생성하면 안되는 Calendar 같은 경우 다른 method를 사용해주어야 한다. 

```
<bean id="" class="java.util.Calendar" factory-method="getInstance"></bean>

Calendar now = (Calendar)applicationContext.getBean("now"); 
```

 필요하다면 init(초기화) , destroy(자원반납) method를 지정해서 사용 가능하다. 

```
<bean id="lg" class="spring.tv.LgTV" lazy-init="true" scope="singleton"
			init-method="init" destroy-method="destroy"/>

-LgTV.java-
public void init() {
		System.out.println("init() 초기화");
	}
public void destroy() {
		System.out.println("destroy() 자원반납");
	}

```

LgTV가 메모리에 뜰때마다 초기화가 될것이다. 

