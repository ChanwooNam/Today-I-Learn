# spring 4

jdbctemplate : 쓰기위해 라이브러리 설정

(maven repository -> springjdbc  -> 4.3.14 복붙  )



dbcp/commons-dbcp -->
		<dependency>
			<groupId>commons-dbcp</groupId>
			<artifactId>commons-dbcp</artifactId>
			<version>1.4</version>
		</dependency>
		<!-- 

복붙....

<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
		<property name="driverClassName" value="oracle.jdbc.OracleDriver"></property>
		<property name="url" value="jdbc:oracle:thin:@127.0.0.1:1521:xe"></property>
		<property name="username" value="scott"></property>
		<property name="password" value="tiger"></property>
	</bean>
	

	<bean id="template" class="org.springframework.jdbc.core.JdbcTemplate">
		<constructor-arg ref="dataSource"></constructor-arg>
	</bean>


@Autowired
	private JdbcTemplate template;

데이터 소스가 있고 생성자를 통해 데이터 소스를 넘겨줘서 탬플릿 객체 잘 생성 되었으면 , UPDATE(),queryForInt(),queryForObject(),query()를 통해 간편하게 데이터를 처리할 수 있다. 



#### mybatis 

교재 467pg

mybatis 는 sqlsesstion 이 필요하고  datasource 사용할 것임

sql구문은 dao_mabatis 에서 안씀 밖으로 나갈것 (매핑?)

SqlSession sqlSession; (라이브러리 구축 필요 )

<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis</artifactId>
			<version>3.4.6</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
		<dependency>
			<groupId>org.mybatis</groupId>
			<artifactId>mybatis-spring</artifactId>
			<version>1.3.2</version>
		</dependency>

pom.xml 복붙



mybatis.org  -> 시작하기 

우리가 만들건 sqlsession, sqlsession 만들어주는건 sqlsessionfactory

3번째 코드 박스

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="${driver}"/>
        <property name="url" value="${url}"/>
        <property name="username" value="${username}"/>
        <property name="password" value="${password}"/>
      </dataSource>
    </environment>
  </environments>
  <mappers>
    <mapper resource="org/mybatis/example/BlogMapper.xml"/>
  </mappers>
</configuration>
```

이거 전문 복붙

src/main/resources => new => xml file (mybitis_config)여기에 복붙 



src/main/resources => new => package => mapper

src/main/resources => new => xml file (이름은 user_mapper(mybitis mapper resource와 같아야함))

```
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
  PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="org.mybatis.example.BlogMapper">
  <select id="selectBlog" resultType="Blog">
    select * from Blog where id = #{id}
  </select>
</mapper>
```

복사 

parameterType="spring.biz.user.vo.UserVO" : ?들어갈 정보도  uservo에 넣어서 오겠습니다.

select * from userinfo where userid=#{userid} and userpwd = #{userpwd}

?에 변수 바인딩 #{}으로 사용한다. 

<!-- user_mapper.xml 에서 간편하게 쓰기위해 type alias 처리 -->





log4j 에

<logger name="user">
        <level value="TRACE"></level>
    </logger>

추가 

콘솔에 돌리면 설명들이 보여짐 syso으로 찍지 않아도 결과 나옴 



searchlist  :  where 절과 hashmap 을 통해서 email 입력하면 key 로   email 먼저 뽑고 value 값을 찾는다. 