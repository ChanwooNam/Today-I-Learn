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





spring_04_web

mavenproject  생성 - webapp 1.0 으로 생성

index.jsp 지움 ,  pom.xml 기존거 카피하면 안됨 build 필요함 build 살리고 잘 카피하면 됨 

buildpath 에서 설정하고 

target runtimes apache tomcat v9.0 check 하고 apply

project facets 에서 자바 1.8버전으로 apply

pom_temp 에서 web servlet  pom.xml에 복사

java application 으로 test01 잘돌아가나 돌려보자 



이제 환경설정 파일이랑 같이 돌아서 rename 안된다.!!

jsp 만들고 

web.xml 수정했음 



프론트 컨트롤러 대문을 하나로 만들어서 관리하자 

홈페이지 또한 서블릿을 너무 많이 배치하고 다 포워딩 하고 하면 관문이 너무 많아짐 -> 유지 보수가 힘들어짐 -> 프론트 컨트롤러 디자인패턴을 입혀야함 

모든 요청을 여기로 받고 요청들을 분석해서 알맞은 결과값을 보내도록 핸들링하는 역활 

​	<url-pattern>/list.do</url-pattern>

<url-pattern>*.do</url-pattern> 이렇게 바꿔서 모든 .do 여기로 들어오게 만든다. 

String uri = request.getRequestURI();
		System.out.println(uri);
		String path = uri.substring(uri.lastIndexOf("/"));
		System.out.println("path" + path);

		if (path.equals("/list.do")) {
		
		}else if(path.equals("/update.do")) {
		
		}

이런식으로 경로를 받아와서 그에 따른 핸들링을 해준다. 

else if 계속 하면 안 좋으니 컨트롤러를 통해 제어하자 

각각 요청에 따라 맞는 것을 수행하는데 그것을 한곳(interface)에서 알아서 list.do or update.do 등이 바인딩 되면서 수행 (다형성!!!)

controller 인터페이스 만들고 listcontroller 클래스(list.do  들어오면 반응할애) 만든다

map 구조를 이용해서 list.do 이면 뭐 , 뭐이면 뭐 이렇게 

HandlerMapping 클래스 만들어서 해보자 



그냥 뒤에 fewfhttp 등 이상한 주소 쓰면 404에러 뜨는데 , web.xml에서 처리했음 