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

{% highlight markdown %}
sudo apt install ./code_1.51.1-1605051630_amd64 .deb
{% endhighlight %}

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
