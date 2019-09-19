# spring 6

spring_03_web

spring_06_web : 강사님 



message_en_properties 만짐

message_ko_properties 메세지 등록



web에 package  생성

validator 

usercontroller 에서 





패키징----------

pom.xml

<build>
		<finalName>chanwoo</finalName>
	</build>

이름 정하기 



마우스 우측, run as, maven install

target 에 chanwoo.war 생성됨 



디플로이

진짜 톰켓 : c에서 tomcat , conf, server.xml ㅈ열어서  69번라인 8080은 오라클 , 80으로 바꿔준다. 

, bin, statup.bat 실행 ,  브라우저 열고, localhost 치기 , 다른 페이지 열어서 <http://localhost/examples/>  : 톰켓에서 제공해주는것  (톰켓폴더에서 webapps있음 )

, 만들어진 war파일 C:\Tomcat\apache-tomcat-9.0.20\webapps 여기에 넣으면 자동으로 추가됨 

<http://localhost/chanwoo/> 치면 들어가짐 



이미지 제출하고 보려하니 안나옴 그이유는 파일이 들어있지않아서?? 자동으로 지워버림 

C:\Tomcat\apache-tomcat-9.0.20\webapps\chanwoo 여기에 수동으로 upload 폴더 만들어주면

처리됨




clean 작업 

rus as , maven clean 



서버라서 shutdown 실행 해야함 bin 에서 



localhost/manager로 들어가면 좀더 자세히 편리하게 관리가능하다 







