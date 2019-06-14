# spring5 



이름위주

//@Autowired
	//@Qualifier("jdbc")
	@Resource(name="mybatis")



타입위주

@Autowired or @inject
	SqlSession sqlSession = null;

@inject 쓰기위해서 mavenrepository => javax.inject=>제일 많은거 => pom.xml에 카피



### interface 설계

mappers package 만들고 UserMapper interface 생성

user_mapper 의 역활을 interface로 바꾸겠다.!!



day03 다이나믹 웹으로 프로젝트 만들고 만들때 generate check!!

<http://tomcat.apache.org/>

document 9

jdbcdatasource => oracle   => 이거뭐 안함



day03 - meta-inf 에 공유해준 context.xml 복사(톰켓 구동될때 컨넥션 만들어줌 이렇게 연결할꺼야 컨넥션 내가 관리할거야 )

day03 -web-inf 에 web.xml에다 공유해준 web.xml에서  resource 태그 복사 

webcontent 에 jstl_sql_context.jsp 복사 ,라이브러리 없어서 에러남 , pom.xml이 없으니 web-inf에 lib에 박으면됨 (maven에서 jstl jar 파일 받아서 lib에 박으면됨)





mavenproject  생성 - webapp 1.0 으로 생성

index.jsp 지움 