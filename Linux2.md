# Linux2 

2일차 6-27 

- 자동완성 
  파일이나 디렉토리의 이름의 일부만 입력한 후 Tap키를 이용해서 완성하는 기능

  ls : 기본적인 파일과 디렉토리의 리스트를 보여주는 명령어
  -a : 옵션으로 숨김파일을 포함한 모든 파일을 보여주기 위한 옵션은 
  -l : 파일에 대한 자세한 사항( 퍼미션, 소유자, 그룹 , 파일크기 등)

	=> ls -al 형태로 많이 이용한다. 

  cat명령을 이용 :파일의 내용을 확인하고 싶을때 간단하게 사용하는 명령어
(ex) cat anacon +Tap(자동완성) ( 자동완성이 가능한 경우에 자동완성 동작 , 자동완성을 할 수 없는 경우 [Tap]을 두번 누르면 anacon으로 시작하는 리스트를 보여준다. )

기본적으로 도스키를 제공 ( 화살표 위, 아래를 이용해서 기존에 사용했던 명령을 다시 이용 가능 )
---------------------------------------------------------
윈도우 시스템의 메모장같은 텍스트 에디터를 사용해 보아요
- gedit  :  메모장 ( 해당 프로그램은 GNOME이라는 윈도우 매니저를 이용하는 		   경우에만 사용이 가능하다. )( gui 환경에서만 사용가능하다, text환경		   에서는 불가) 
- vi : 터미널 모드인 경우 전통적으로 vi라는 에디터를 사용
	 2가지 모드가 있어요 
	입력모드가 있고 ex 모드가 있어요~ 
	입력모드에 진입하기 위해서는 i key나 a key 사용.
	  insert모드(i:현재커서에서 입력모드 , a: 현재커서다음에서 입력모드), 
	ex모드에 진입하기 위해서는 exc key 사용
	ex모드에서는 한글자 삭제(x), 한줄 삭제(dd), 한줄 복사(yy), 여러줄 삭제(숫자 dd), 여러줄 복사(숫자 yy), 붙여넣기(p)
	  ex모드( esc키 , 저장-> : w, x: 현재 커서에서 한 글자 지우기, dd: 한 라인 지우기, 	  yy: 한줄 복사, p:붙여넣기, 원하는 복사 줄수 + yy: 여러줄 복사(복사를 원하는 첫째줄 마지막에서 한칸띄운 곳에서 ) : wq -> 자장하고 나옴 :q! -> 그냥 나옴)
- !v 현재 히스토리에서 가장 최근 것부터 찾기 시작해서  v로 시작하는걸 찾아서 실행해 
- window + space : 한글 전환 

- startx : ctrl+alt+f2 하면 프롬프트 화면이 나오게 되는데 여기서도 우리 같은 end유저가 편하게 사용하기 위한 window 시스템처럼 gui 시스템 xwindow 시작

-----------------------------------------------------------------------
마운트라는 개념

마운트 : 물리적인 장치( 하드디스크 , CD, DVD, USB )들을 사용하기 위해서 
		 특정한 위치( directory) 에 연결시켜 주는 것을 마운트 한다 라고 함

CD/DVD에 대한 장치 이름 => /dev 안에 cdrom이라는 이름으로 잡혀있어요 
현재 자동으로 마운트된 CD/DVD의 위치는 /run/media/userid/cdtitle 이곳이고 이런 형태로 마운트 된다. 

현재 자동으로 mount가 되어 있는데 mount를 헤제 
그냥 cd + enter : 사용자의 home directory로 이동한다. 
# umount /dev/cdrom(/dev/sr0) 

이번에는 특정 mount point(directory)를 이용하여 
CD/DVD를 mount 해보아요
# mkdir (make directory) mycdrom (directory 이름)

마운트 명령을 이용해서 CD/DVD를 특정 directory와 연결
# mount -t iso9660 (type) /dev/cdrom(원본여기야) /root/mycdrom(이 directory에 연결할거야)
------------------------------------------------------------------
ISO 파일을 제작해서 mount해서 사용해 보아요
ISO파일(.iso) : 국제표준기구(ISO)가 표준으로 제정한 광항 디스크 압축 파일
Linux에서는 이런 iso파일을 쉽게 만들수 있어요
사용하는 프로그램은 genisoimage
해당 프로그램이 우리 시스템에 설치가 되어 있는지부터 확인. 
RPM(RedHat Package Manager)을 이용해서 해당 프로그램(package)가 설치되어 있는지를 확인 
=> # rpm -qa genisoimage 
현재 설치되어 있어요!!

이 프로그램을 이용해서 /boot 디렉토리의 내용을 iso파일로 압축할거에요
# genisoimage -r(대소문자 구분) -J(8글자 이상) -o(아웃풋) boot.iso(생성할 이름) /boot(어떤걸 ISO파일로 만들거니)

-----------------------------------------
필수 명령어
1. ls (list) : 파일과 디렉토리의 목록을 출력하기 위해 일반적으로 사용하는 옵션은 -al을 많이 사용
2. cd (change directory) : working directory를 이동하기 위해서 사용.
	- cd 명령에 인자를 주지 않으면 현재 사용자의 home directory로 이동한다.
	- . : 현재 디렉토리 , .. : 상위 디렉토리 
3.pwd ( print working directory ) : 
4. rm : 파일이나 디렉토리를 지울때 사용
	    많이 사용하는 옵션은 -rf를 이용 
		-r : ( 재귀적으로 특정 디렉토리 그 안에 디렉토리들을 삭제할때 사용)
		-f : force (강제적으로)
		# rm -rf /root/myiso
5. cp : copy의 약자로 파일이나 디렉토리를 복사할 때 사용
	    # cp abc.txt ( 원본 ) bbb.txt ( 복사본 )
6. touch : 파일 크기가 0인 파일을 생성할 때 사용 
			# touch newfile
			=> newfile이라는 파일이 없는 경우 파일 사이즈가 0일 파일이 생성
			=> 현재 newfile이라는 이름의 파일이 있는 경우에는 해당 파일의 				수정 날짜를 현재 날짜로 변경함
7. mv : move의 약자로 파일을 이동할 때 사용, 파일이나 디렉토리의 이름을 변		경할 때 사용
		
		# mv aaa.txt bbb.txt 
8. mkdir : make directory. 새로운 디렉토리를 생성  
9. rmdir : rm directory. 디렉토리를 삭제하기 위한 명령
			단, 디렉토리안에 파일이나 다른 디렉토리가 없어야 해요. 
			( 그냥 rm 명령을 이용해서 사용하는 것이 편하다 )
10. cat : concatenate. 텍스트로 작성된 파일의 내용을 출력
11. head, tail : head는 텍스트 파일의 상위 10줄, tail은 텍스트 파일의 하위 10줄 				출력
12. more : cat과 유사한 기능, 텍스트 파일을 페이지 단위로 출력 space 바를 누			르면 다음 페이지로 넘어간다. 
13. clear : terminal 깨끗이 지워요 

============================================

사용자와 그룹과 퍼미션

- 리눅스는 다중 사용자 시스템 
- 기본적으로 root라는 이름의 super user가 존재한다. 
- 모든 사용자는 특정 그룹(소속)에 속해 있어요. 
- 리눅스 시스템의 모든 사용자는 /etc/passwd 파일에 정의 되어 있어요
  # cat /etc/passwd 
	시스템 내에 필요한 많은 사용자들이 있는 것을 확인 할 수 있다
	root    : x            : 0         : 0      : root               : /root        : /bin/bash	
	아이디 : 패스워드   : 사용자id :그룹id : 사용자전체이름 : 홈 디렉토리 : 기본 쉘(명령어 해석기)
 #  cat /etc/shadow
	패스워드가 암호화되서 들어가 있어요.  
 #  cat /etc/group
	root    : x   : 0:
	그룹명 :      : 그룹id

- 새로운 사용자 추가 ( root 라는 super user만 추가 가능하다. ) 
	# useradd testuser( 사용자이름 ) : testuser라는 이름의 사용자를 추가 , 자동으로 testuser라는 										그룹이 추가되고 거기에 속하게 됨
	=> 새로운 사용자 추가할 때 특정 옵션을 이용하지 않고 사용자를 추가하게되면 사용자 id는 			마지막 사용자 ID에 +1해서 생성되게 되요!!
	# useradd -u 1111 testuser : 사용자를 추가할 때 특정 사용자의 ID를 사용할 수 있어요!
	# useradd -g root testuser : 사용자를 추가할 때 사용자의 그룹을 root 그룹으로 추가. (group									은 새로 만들지 말고 기존 그룹에 포함시킬거야)
	# useradd -d /newhome testuser : -d 옵션을 주지 않으면 기본적으로 일반 사용자의 홈 디렉											토리는 /home/testuser로 잡여요

	# 실습
	# useradd -g centos testuser
	=> 새로운 사용자 추가 성공
	# 아직 로그인은 할 수 없어요 ( 비밀번호 설정을 안했어요 )
	# passwd testuser
	=> 비밀번호 설정
	# 가상 콘솔로 로그인이 되는지 확인해보자 
	=> 로그인 성공!!
=====================================================
	사용자의 정보를 수정하려면?	( id, group, home directory 등..)
	# usermod -g root testuser 
	사용자를 삭제하려면?
	#userdel -r testuser
	
	=> -r 옵션을 주면 해당 사용자의 홈 디렉토리도 같이 삭제
	======================================================

파일과 디렉토리의 소유와 퍼미션

-rw-r--r--.  1 root root     12288  6월 27 19:26 .sample.txt

1. 맨 앞에 1칸은 이 파일의 종류를 지칭한다. 
	- : 파일을 지칭
	d : directory를 지칭
	l : 링크(심볼릭링크)를 지칭
	
2. 그 뒤에 9칸은 해당 파일(디렉토리)의 퍼미션을 지칭
	rw-                 r--                r--  
	소유자의 퍼미션  그룹의 퍼미션  other의 퍼미션
	421 ( 4 와 2 사용 rw-의 자리값은 6 ) : 숫자로 퍼미션을 표현할 수 있다. 
	r : readable ( 읽을 수 있는 )
	w : writable ( 수정할 수 있는 )
	x : excutable ( 실행할 수 있는 )
	각각의 퍼미션에 대해 어떤 것을 할 수 있는지 보여준다.
	앞에 있는 것은 주인 => root라는 사용자가 주인이고 뒤에는 group => root라는 그룹
	즉, root는 읽고 쓸수 있지만 실행은 못함, root그룹은 읽는것만 가능 수정x 실행x,
					rw-				--- : 이렇게 되면 소유자나 그룹에 속해있는 사람이 아니면 파											일을 읽거나 수정하거나 실행 못한다.

[root@localhost ~]# ls -al
합계 137688
d	r-x	r-x	---. 16 root root      4096  6월 27 21:46 .
소유주는 현재 디렉토리 읽을수 있고 실핼할 수 있다( 들어올 수 있다 ), 소유자나 그룹이 아닌사람은 이 안으로 들어올 수 조차 없다.
centos:x:1000:1000:centos:/home/centos:/bin/bash
centos는 root 사용자도 아니고  root 그룹도 아니고 other 사용자 이기에 들어갈 수 없다. 
	# usermod -g root centos : centos의 그룹을 root로 바꾼다.
	=> /root 로 들어올 수 있다. 

파일의 퍼미션 변경!!
-rw-r--r--.  1 root root     12288  6월 27 19:26 .sample.txt
=> 소유자와 같은 그룹의 사람만 해당 파일을 읽거나 수정이 가능한 상태로 만들고 실행은 안되게 	설정하고 싶어요
=> rw- rw- --- ( 660 )
	# chmod 660 sample.txt

파일의 소유자와 그룹을 변경할 수 있다!
	#chown centos sample.txt => 해당 파일에 대한 소유자를 변경
	#chown centos.centos sample.txt => 해당 파일에 대한 소유자와 그룹을 동시에 변경
	#chgrp centos sample.txt => 해당 파일에 대한 그룹만 변경

리눅스, 유닉스 시스템의 자료구조 
inode : inode 블록안에 inode 객체가 있고 파일에 대한 정보가 있음, inode가 실제 데이터를 point 하고 있음, 가르키고 있음, 실제 데이터는 다른곳( 데이터 블록 )에 저장되어 있음 
각각의 파일은 inode를 point 하고 있다. 심볼릭링크는 inode를 통해 링크구나 라는것을 알고 inode가 데이터 블록에 원본 파일 포인터를 가르키고 원본 파일 포인터가 원본 파일을 가르킨다.  