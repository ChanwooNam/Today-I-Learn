# Big data introduction

< 빅데이터 분석 >

- 개발 환경설정
	python언어를 이용 
	python 개발을 할때 가장 일반적인 개발툴 : 파이참
	python 데이터 분석을 할때 가장 일반적인 개발툴 : 주피터 노트북 
	
- 1단계. python language spec.
	=> 프로그램 작성에 대한 연습문제  
  2단계. python 데이터분석 library 
	=> numpy & pandas 사용방법
  3단계. machine learning
  4단계. deep learning 

- python 설치 
	개별적으로 설치하는 것보다는 개발툴 + 인터브리터 + 각종 라이브러리가 합쳐져있는 
	anaconda라는 걸 설치해서 사용
	www.anaconda.com/ditrubution/
	3.7버전 다운로드 
	 	(작업관리자 서비스에서 oracleserviecexe 수동으로 바꿔서 중지 메모리 많이 잡아 먹어서 
	- 설치 완료 후
	anaconda prompt , 관리자 권환으로 실행 
	-pip upgrade
	pip라는 패키지 설치 도구가 있는데 이 pip를 최신 버전으로 업그레이드
	=> python -m (-m : python interpiriter 를 통해서 외부프로그램 실행)
	=> python -m pip install --upgrade pip
	
	- 가상 환경 설정
		우리가 나중에 사용할 tensorflow 이용할건데 
		=>현재 tensorflow는 python3.6버전 이전에서 동작 
		=> conda create -n cpu_env(가상환경이름) python=3.6 openssl
		현재 존재하는 가상환경의 리스트 출력