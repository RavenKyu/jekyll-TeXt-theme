---
title: "virtualenv - 파이썬 가상 환경 구축"
tags: Python
---

## 왜 필요한가?

### 독립적인 환경을 만들어서 의존성에서 자유로워진다.

파이썬으로 개발을 진행하다 보면 필요에 따라 서드파티 모듈을 설치하거나 업데이트를 할 수 있다. 하나의 개발 환경에서 개발하는 파이썬 프로젝트가 많다면 개발 시간에 따라 모듈별로 버전의 차이가 발생하게된다. 어떠한 프로젝트는 개발 당시의 환경과 많이 달라져있을 수 있다. 동작하지 않거나 예기치 않는 결과 값을 만들 수 있다. 또는 전체 시스템에도 중대한 문제가 발생할 수도 있다.

virtualenv를 이용하여 **개발 환경을 프로젝트별로 분리하여 완전히 분리된 독립적인 환경을 만들어 사용**할 수 있다. 현재 사용중인 파이썬 환경을 그대로 복사하거나 새롭게 구성하여 사용할 수 있다. **분리된 가상환경은 다른 프로젝트에 설정된 가상환경에 어떠한 영향도 미치지 않는다.**

---

## 사용 방법

### 가상 환경 공간 만들기
설치된 환경에 따라 실행 방법의 차이가 있을 수 있다.

`python3 -m virtualenv mytestenv`

성공적으로 가상 환경 공간을 만들었다면 아래 메세지를 출력해 준다. 

	Using base prefix '/Library/Frameworks/Python.framework/Versions/3.4'
	New python executable in mytestenv/bin/python3
	Also creating executable in mytestenv/bin/python
	Installing setuptools, pip, wheel...done.

* `/Library/Frameworks/Python.framework/Versions/3.4` 에 설치되어 있는 파이선을 기본으로 만들었다.
* 현재 디렉토리로 부터 `mytestenv/bin/`에 python3 와 python 로 **파이썬을 실행할 수 있도록 실행파일을 생성**해 두었다.
* 필요한 모듈들을 네가 **나중에 쉽게 설치 할 수 있도록 setuptools, pip, wheel 등을 미리 설치**했다. 

위 메세지에는 빠져 있지만 virtualenv는 기존의 파이썬 환경과 가상환경에 편하게 오갈 수 있도록 도와줄 '쉘 스크립트'를 `mytestenv/bin/`에 생성해 두었다. 

### 가상 환경 활성화 하기
`mytestenv/bin/activate` 를 source 명령어를 이용해서 실행하면 가상 환경의 위치에 맞게 환경변수를 변경하게 된다.

`source mytestenv/bin/activate`

위의 명령을 실행하면 별 말 없이 실행되며 이용중인 가상 환경의 이름이 계속 프롬프트에 붙어있게 된다.

{% highlight bash %}
(mytestenv)
raven@imdeoggyuui-MacBook-Pro ~
  %                                                                                  
{% endhighlight %}

가상 환경 mytestenv으로 잘 들어왔다는 것을 뜻한다. 이제 `python` 또는 `python3`를 입력하여 버전 또는 바뀐 환경변수등을 확인해 보자.

#### 가상 환경 변환전의 파이썬 상태 확인
명령어 `python`을 입력하여 실행하면 아래와 같이 2.7.10 버전의 파이썬이 실행된다. 

	raven@imdeoggyuui-MacBook-Pro ~
	  % python                                                                          !
	Python 2.7.10 (default, Jul 14 2015, 19:46:27) 
	[GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.39)] on darwin
	Type "help", "copyright", "credits" or "license" for more information.
	>>> 
	
`python3`을 실행하여 가상 환경 변환전의 환경변수를 확인한다.

	raven@imdeoggyuui-MacBook-Pro ~
	  % python3                                                                         !
	Python 3.4.3 (v3.4.3:9b73f1c3e601, Feb 23 2015, 02:52:03) 
	[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
	Type "help", "copyright", "credits" or "license" for more information.
	>>> import sys
	>>> sys.path
	['', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python34.zip', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/plat-darwin', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/lib-dynload', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/site-packages']
	>>>  

#### 가상 환경 변환 후, 파이썬 상태 확인
`python` 을 입력하여 실행하니 아까와는 다르게 버전이 3.4.3 인 것을 확인 할 수 있다. 또한 파이썬의 환경변수 역시 가상환경의 경로로 바뀌어 있음을 알 수 있다.

	(mytestenv)
	raven@imdeoggyuui-MacBook-Pro ~
	  % python                                                                          
	Python 3.4.3 (v3.4.3:9b73f1c3e601, Feb 23 2015, 02:52:03) 
	[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
	Type "help", "copyright", "credits" or "license" for more information.
	>>> import sys
	>>> sys.path
	['', '/Users/raven/mytestenv/lib/python34.zip', '/Users/raven/mytestenv/lib/python3.4', '/Users/raven/mytestenv/lib/python3.4/plat-darwin', '/Users/raven/mytestenv/lib/python3.4/lib-dynload', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4', '/Library/Frameworks/Python.framework/Versions/3.4/lib/python3.4/plat-darwin', '/Users/raven/mytestenv/lib/python3.4/site-packages']
	>>> 

### 가상 환경 비활성화 하기
가상 환경에서 나오는 명령어는 매우 간단하게도 `deactivate` 이다.

	(mytestenv)
	raven@imdeoggyuui-MacBook-Pro ~
	  % deactivate                                                                      !
	
	raven@imdeoggyuui-MacBook-Pro ~
	  %                             

---

## 가상 환경 활용하기
이제는 시스템에 설치된 파이썬을 건드리지 않고 가상 환경에서 마음껏 라이브러리를 설치해볼 수 있다. 새로운 프로젝트를 시작하면 새로운 환경을 또 만들 수 있으므로 항상 같은  환경에서 작업이 가능해졌다.

