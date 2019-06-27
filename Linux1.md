6-26 : 리눅스 시작
1.linux
2.빅데이터 학습준비 -> pytion numpy pandas
3 머신러닝(tenserflow)
3.빅데이터 저장 -> 하둡
4.빅데이터 분석 -> R
5.안드로이드
6 IoT(아두이노)

블로그에 정리

CentOS의 활용

1. vmware player 설치
vmware player -> workstation player 누르고 다운
재부팅하고 실행
i will install the ~~ 클릭 ,리눅스 클릭, centos7 63bit 선택 , location : 바탕화면에 CentOS폴더 만들고 선택, single file 선택

centos download - 맨위에것 다운 
vmware에서 CenOS 만들고 오른쪽 클릭 세팅 -> cd/dvd -> connectrion 에서 use iso ->  cenos (4GB) 위치 알려주고 ok - 가상머신 다시 시작하고 맨위 install 해준다. -> 언어선택 -> 소프트웨어 선택 : 개발 및 창조 클릭 , 설치 대상 : 파티션을 설정 체크 -> 여기를 클릭하여 자동으로~ 클릭 -> 변경사항 적용 -> 네트워크 & 호스트 이름 : 켬으로 -> 설치 시작 -> root 암호 설정(gmail 암호) -> 사용자 생성 : 성명 centos , 비번 (gmail 암호) -> 

root 로 관리자 계정 들어가기
한국어(hangle), 위치정보 사용x, 온라인계정 건너뛰기 
오른쪽버튼 누르고 terminal 열기 

바탕화면 centos 파일 있는것을 어딘가 복사 하면 백업이 된것임 , 이것을 이용하면 시스템 이상해져도 돌아올수 있음 
벡업파일 하나 만들어서 복사해두자 
-------------------------------------------------------------------
virtualbox download 
window host로 받으면됨 
실행 - 새로 만들기 - LINUX , redhat 64 bit - 다 default -> 설정 - 저장소 - sata 남기고 지우기 -> sata에서 centos 추가 
---------------------------------------------------------------------
오전
- vmware player 5 설치 
	- 가상머신 소프트웨어(vmware, virtual box)
	- vmware workstation(유료)
	- vmware workstation player(무료)
	- host os , guest os(가상 컴퓨터)
 	- 최신버전의 cpu에서는 player 5 사용 못함
오후
- GNU - GPL
- 필수 개념과 명령어
	- Terminal 실행 
	- 종료 : shutdown -P now 
               halt -p
			init 0 ( runlevel )
	-재시작 : shutdown -r now
			  reboot
			  init 6 
		-로그아웃 : exit	 
				logout
- 가상 콘솔 
	- ctrl + alt f1 ~ f6
-RunLevel : init명령어 뒤에 붙는 숫자를 의미
			RunLevel 숫자마다 의미가 정해져 있다.
			0 :  종료모드
			1 : 시스템복구모드
			2~4 : Text기반 다중 사용자 모드
			5 : 그래픽기반 다중 사용자 모드
			6 : reboot
- PWD ( print working directory ) : 현재 작업 공간
- cd ( change directory )
- 터미널을 실행시킨 후 working directory를 
	/lib/systemd/system로 이동 
- ls ( list ) : 현재 directory 안의 파일이나 목록을 출력
  ls -al
  ls -al runlevel* : runlevel로 시작하는 것만 보여줌 
- /lib/systemd/system 안의 runlevel* 을 li 출력 
- 처음 부팅시 어떤 runlevel로 실행할지를 지칭하는 링크(바로가기) 있음 => /etc/systemd/system/default.target
	cd /etc/systemd/system
	 ls -al de* => default target 있는걸 확일 할수 있음
	ln -sf 지칭되는 곳(/lib/systemd/system)
	ln -sf /lib/systemd/system/multi-user.target /etc/systemd/system/default.target 입력 
	원상복귀 
	ln -sf /lib/systemd/system/graphical.target /etc/systemd/system/default.target