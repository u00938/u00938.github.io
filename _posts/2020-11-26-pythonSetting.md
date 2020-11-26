---
title: python 환경설정(우분투)
layout: post
categories: [Python]
description: ""
customexcerpt: "python - setting"
comments: true
---

* hello
{:toc}


## Visual Studio Code ##
![VSC](/assets/img/vsc.png)
- 코드 에디터 [Visual Studio Code](https://code.visualstudio.com/)
- 우리는 우분투를 쓰기 때문에 .deb 파일을 다운로드 한다.

<br>

- 다운 받은 파일 확인하기! 직접 다운로드 폴더를 열거나, 터미널의 ls 명령으로 확인할 수 있다.
![deb](/assets/img/vsc2.png)
<br>

- 터미널에서 다운받기!(deb파일의 버전을 그대로 입력한다)
<br>

```
~$ sudo apt install ./code_1.51.1-1605051630_amd64 .deb
```

<br>

## 파이썬 버전 확인 후 업데이트하기 ##

```
~$ python2 -V
Python 2.7.18
```

```
~$ python3 -V
Python 3.8.5
```
- python2와 python3가 둘 다 설치되어 있다.
- 우선 현재 파일이 어떤 것인지 확인하기 위해 `which python` 명령으로 파일의 위치를 확인한다.

```
~$ which python
/usr/bin/python
```

<br>

- `ls -al` 명령어로 이 위치의 파일이 어떤 파일을 가리키는지 확인해본다.
- 현재 python2를 사용 중인 것으로 확인되었다. 이제 이것을 python3로 바꿔줄 것이다.

```
~$ ls -al /usr/bin/python
lrwxrwxrwx 1 root root 7  4월 15  2020 /usr/bin/python -> python2
```

<br>

- `ls` 명령어로 현재 설치된 python 파일들을 확인해본다.

```
~$ ls /usr/bin/ | grep python
dh_python2
python
python2
python2.7
python3
python3-config
python3-futurize
python3-pasteurize
python3.8
python3.8-config
x86_64-linux-gnu-python3-config
x86_64-linux-gnu-python3.8-config
```

<br>

- `update-alternatives --install` 명령어를 통해 실행파일을 등록한다. 맨 끝에 붙인 숫자(1/2)는 우선순위

```
~$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
~$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 2
```

<br>

- `update-alternatives --config python` 명령어를 입력하면 등록된 실행파일을 선택할 수 있는 메뉴가 나온다.
![python](/assets/img/p10.png)

<br>

- 원하는 메뉴 번호를 입력한다. 나는 python 3.6으로 업그레이드 하는 것이 목적이기 때문에 2 입력!

<br>

- 현재 사용중인 파일을 확인해본다.

```
~$ ls -al /usr/bin/python
lrwxrwxrwx 1 root root 24 11월 26 18:56 /usr/bin/python -> /etc/alternatives/python
```
```
~$ ls -al /etc/alternatives/python
lrwxrwxrwx 1 root root 18 11월 26 18:56 /etc/alternatives/python -> /usr/bin/python3.8
```

<br>


## python 환경설정 ##
1. 새 폴더에 파일을 만든다. .py로 파이썬 파일을 만들 수 있다.
![VSC](/assets/img/p1.png)
<br>

2. 파이썬 익스텐션을 다운받는다.
![VSC](/assets/img/p2.png)
<br>

3. 코드를 실행시키기 위해 Run(벌레모양) -> Run and Debug(혹은 Debug with Python) -> Python file 
![VSC](/assets/img/p3.png)
![VSC](/assets/img/p4.png)

- "Select Python Interpreter" 창이 뜨면 클릭해서 설치해준다. (설치한 python 버전을 선택해주면 된다)

<br>

4. 매번 이 과정으로 코드를 실행시킬 순 없으므로 좀 더 간편하게 하기 위해 json파일을 설치한다. 

- "create a launch.json file"을 클릭하면 json 파일이 생성된다. 

![VSC](/assets/img/p5.png)
![VSC](/assets/img/p6.png)
<br>

5. 코드를 실행시키는 방법 

- 코드를 실행시키기 전 저장하는 것을 잊지 말자! (CTRL + S)
- 코드를 실행하는 방법은 4가지가 있다.

![VSC](/assets/img/p7.png)

<br>

- 마지막 방법이 제일 간편하다. ^^! 버튼 하나만 누르면 끝!

![VSC](/assets/img/p8.png)

<br>

## pip 설치하기 ##
- 파이썬으로 작성된 다양한 라이브러리 패키지를 이용할 수 있다.
- pip(package installer) : 패키지 관리자
- 현재 python3을 사용하고 있으므로, pip3를 설치할 것이다.

```
~$ sudo apt install python3-pip
```
<br>

- pip 버전을 확인해보자

```
~$ pip3 -V
pip 20.0.2 from /usr/lib/python3/dist-packages/pip (python 3.8)
```

<br>

- pip를 최신 버전으로 업그레이드

```
~$ pip3 install --upgrade pip
```

<br>

- 현재 설치되어있는 패키지 내용을 볼 수 있다.

```
~$ pip3 list
Package                Version             
---------------------- --------------------
apturl                 0.5.2               
bcrypt                 3.1.7               
blinker                1.4                 
Brlapi                 0.7.0               
certifi                2019.11.28          
chardet                3.0.4               
...

```

<br>

- 패키지 정보 확인하는 명령 `pip3 show 패키지이름`

```
~$ pip3 show apturl
Name: apturl
Version: 0.5.2
Summary: UNKNOWN
Home-page: UNKNOWN
Author: UNKNOWN
Author-email: UNKNOWN
License: UNKNOWN
Location: /usr/lib/python3/dist-packages
Requires: 
Required-by: 
```

<br>

- 패키지 설치 `pip3 install 패키지이름`
- 패키지 업그레이드 명령 `pip3 install --upgrade 패키지이름`
- 패키지 삭제 명령 `pip3 uninstall 패키지이름`
