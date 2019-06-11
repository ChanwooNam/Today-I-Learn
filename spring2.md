# spring 2

applicationcontext 는 곧 spring 

## 스키마 기반 환경설정

일일이 환경설정

### injection 

생성자 injection : constructor-arg (dao정보가 반드시 필요한데 , 생성자를 통해 주입 시켜준다.) 

파라미터 하나짜리 생성자를 넘겨준것 생성자가 jdbc기반으로 수행될것이다. 

- ```xml
  <bean id="jdbc" class="spring.biz.user.dao.UserDAO_JDBC"></bean>
  <bean id="spring" class="spring.biz.user.dao.UserDAO_Spring"></bean>
  <bean id="mybatis" class="spring.biz.user.dao.UserDAO_MyBatis"></bean>
  	
  <bean id="userservice" class="spring.biz.user.service.UserServiceImpl">	
  		<constructor-arg ref="jdbc"></constructor-arg>	
  </bean>
  ```

- ``` xml
  <constructor-arg ref="spring"></constructor-arg>
  <constructor-arg ref="mybatis"></constructor-arg>
  ```

  위처럼 간편하게 환경설정만 변경해서 바꿀 수 있다. 

setter injection : property

​	마지막 열을 통해서 mybatis가 끊어지고 jdbc로 된다. 

​	UserServiceImpl에 반드시 setDao 함수가 있어야 한다. 

- ``` xml
  <bean id="jdbc" class="spring.biz.user.dao.UserDAO_JDBC"></bean>
  	<bean id="spring" class="spring.biz.user.dao.UserDAO_Spring"></bean>
  	<bean id="mybatis" class="spring.biz.user.dao.UserDAO_MyBatis"></bean>
  	
  	<bean id="userservice" class="spring.biz.user.service.UserServiceImpl">
  		<constructor-arg ref="mybatis"></constructor-arg>
  		<property name="dao" ref="jdbc"></property>
  	</bean>
  ```

### parameter 넘기기 with index

``` xml
<bean id="user01" class="spring.biz.user.vo.UserVO"></bean>
```

``` java
System.out.println( context.getBean("user01") );
```

defalt생성자가 수행되면서 전부 null이다.  injection을 통해서 parameter를 넘겨보자 

```xml
<bean id="user01" class="spring.biz.user.vo.UserVO">
		
		<constructor-arg index="1" value="홍길"></constructor-arg>
		<constructor-arg index="2" value="1234"></constructor-arg>
		<constructor-arg index="0" value="java"></constructor-arg>
		<constructor-arg index="4" value="7777"></constructor-arg>
		<constructor-arg index="5" value="서울"></constructor-arg>
		<constructor-arg index="3" value="ddd@"></constructor-arg>
		
</bean>
<bean id="user02" class="spring.biz.user.vo.UserVO">
		<property name="address" value="서울"></property>
		<property name="username" value="서울"></property>
		<property name="phone" value="77"></property>
		<property name="userpwd" value="1234"></property>
		<property name="userid" value="jjjj"></property>
   </bean>
```

생성자injection인 경우 전부 string type이기 때문에 넘기는 순서가 중요하다. 순서에 알맍는 값들을 넘겨주면 되지만, 그렇지 못했다면 위처럼 index로 순서를 주어서 넘기면된다. 

setter injection인 경우 name을 입력 가능하다 순서를 맞출필요 없다. 

ref는 레퍼런스 같은것 , value는 기본형

 list, set,map, properties 타입 매핑 : 책 pg86~



```
<bean id="userservice" class="spring.biz.user.service.UserServiceImpl"
			autowire="byType">
```

같은 type 세가지가 있다. bytype은 이런 에로사항이 있다. 

byname, default

다 setter injection 으로 동작한다. 
		autowire="default" :  autowire="byName" 이다. 
		autowire="byName" : dao라는 이름을 찾는데 dao가 없어서 mybatis를 dao로 바꾸면 동작한다. 
		autowire="byType" : userserviceimple setdao를 통해정보가 주입되야해 너가 알아서 너가 관리하고 있는것들 
		중에 가능성있는걸 찾아서 타입맞춰서 넣어봐 
		근데 jdbc,spring,mybatis 세가지나됨 -> 에러 떨어짐(expected single matching bean but found 3: jdbc,spring,mybatis) 
		

## 어노테이션 기반 환경설정

@component, @service 등 역활에 따라 나눠서 사용한다. 

<context:annotation-config></context:annotation-config>

<context:component-scan base-package="spring.biz"></context:component-scan>

spring.biz 밑에있는 @component 마킹되엤는애들 다 메모리에 띄워줘

   service에 값안넣었으니 당연히 nullpointexception에러가 난다. dao 주소 넣어야함
	UserServiceImpl에 @Autowired, @Qualifier("jdbc") 통해서 해결



​	@Autowired

 bytype으로 동작한다. -> jdbc,spring, mybatis 3가지나 있어서 에러난다

(jdbc,spring,mybatis 세가지나됨 -> 에러 떨어짐(expected single matching bean but found 3: jdbc,spring,mybatis)




​	@Qualifier("jdbc")

dbc,spring  중  고르게 해줘야함




​	@Resource(name = "mybatis")

resource로 위 두개를 한번에 표현





test05_servcice에서 

@Before
	public void setUpBeforeClass() throws Exception {
		

		UserDAO dao = new UserDAO_JDBC();
		service = new UserServiceImpl(dao);
	}
지우고

@runwith : spring이 테스트하게 만들라고

<dependency>
    	<groupId>org.springframework</groupId>
   	 	<artifactId>spring-test</artifactId>
    	<version>4.3.10.RELEASE</version>
	</dependency>

pom.xml에 추가 ->maven dependencies 에 spring-test~~ 추가될것이다.

test05_servcice에서 

@RunWith(SpringJUnit4ClassRunner.class)

@ContextConfiguration(locations = {"classpath:user.xml"})



UserService service;	위에 @Autowired 추가



spring_02 프로젝트 

src/main/java 오른쪽클릭하고 new - sourcefolder

folder name : src/main/resources

src/main/resources : 모든 환경설정 파일은 여기서 관리 , 자바클래스 이외의 자원관리

src/main/resources에서 spring bean configulation file 이름 applicationcontext로 bean,context,p 체크해서 만든다 