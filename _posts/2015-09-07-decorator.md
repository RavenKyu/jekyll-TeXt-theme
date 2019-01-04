---
layout: post
title: 파이썬 장식자(Decorator)
tags: [Python]
category: Python
comments: yes
excerpt: 함수선언문 위에 `@`로 시작하는 것. 어떤 함수의 기능을 변형하기 위해 감싸는 함수(Wrapper)를 만들다 보니 길어진 코드를 짧게 줄이는 용도로 만들어졌다. 
toc: true
---

## 파이썬 장식자(Decorator) 요약

> 데코레이터는 어떻게 생긴건가?

{% highlight json linenos %}
	@decorator
	def foo:
		pass
{% endhighlight %}

위의 코드 처럼 흔히 함수선언문 바로 위에 **`@` 로 시작하는 함수 이름**이다. 

> 데코레이터는 무엇인가?

함수 A가 다른 함수 B를 인자로 받아서 목적에 따라 합쳐진 새로운 기능의 함수를 만들어 낸다. 비유를 하자면 게임에 있는 **'불 속성 구슬, 번개 속성 구슬(함수 A)'을 무기(함수 B)에 장착하면 해당 속성의 추가 데미지가 생기는 것**과 비슷하다. 

> 파이썬 장식자를 꼭 사용자 모두가 알아야 하는가?

아니다. 라고 말할 수 있을거 같다. 장식자를 모르면 그 것이 없음에 대한 불편조차 모르고 필요에 따라 비슷하게 만들어 쓸 뿐이다.

> 장식자가 만들어진 동기는 무엇인가?

**어떤 함수의 기능을 변형하기 위해 감싸는 함수(Wrapper)를 만들다 보니 길어진 코드를 짧게 줄이는 용도**로 만들어졌다. 

___

## 장식자 만들기

### 장식자의 구현 원리
파이썬에서는 함수 또한 객체로 취급한다. 아래 예제에서 함수 deco()는 함수이름을 인자를 받아 **기능이 추가된(꾸며준) 함수 이름을 리턴**해 준다. 마지막줄인 `func = deco(func)` 즉, deco()를 통해 기능이 추가된 함수로 변경되게 된다.

위에서 언급했던 칼에 마법 구슬을 장식(Decoration) 해보자. 여기서 **칼은 func, 마법 구슬은 deco** 라 하겠다.

	def deco(f): 
		def new_func():  # 추가 기능을 가진 함수 정의
			'''마법구슬의 속성 데미지를 추가''' 
			f()  # 인자로 받은 func() 함수
			print('불 속성 데미지 15를 추가로 주었다!!')
	    return new_func  # new_func 함수 이름을 반환
	
	def func():  # 목적 함수
		print('칼을 휘둘러 데미지 30을 주었다!!')
	
	func = deco(func)  
	
위 코드를 장식자를 이용하여 작성하면 아래와 같다. 위 코드와 아래의 코드는 같은 일을한다.
 	
	def deco(f):
		def new_func():
			# 위와 동일한 코드
	    return new_func
	
	@deco  # `func = deco(func)` 대신 목적 함수 위에 바로 써 준다.
	def func():
		print('칼을 휘둘러 데미지 30을 주었다!!')
	    
이제 장식자를 붙이지 않은 func() 함수의 결과 값과 장식자를 사용한 func() 함수의 결과 값을 비교해 보자.

#### 장식자 사용하지 않은 함수
장식자로 사용할 함수는 구현했으니 func()함수에서 장식자를 사용하지 않은 경우이다. 우리가 기대했던 대로 순수히 func() 함수를 실행했다.

	>>> def deco(f):
	...     def new_func():  # 추가 기능을 가진 함수 정의
	...         '''마법구슬의 속성 데미지를 추가'''
	...         f()  # 인자로 받은 func() 함수를 호출
	...         print('불 속성 데미지 15를 추가로 주었다!!')
	...     return new_func  # new_func 함수 이름을 반환
	... 
	>>> def func():  # 목적 함수
	...     print('칼을 휘둘러 데미지 30을 주었다!!')
	... 
	>>> 
	>>> func()
	칼을 휘둘러 데미지 30을 주었다!!

#### 장식자를 사용한 함수
func()함수 선언시 바로 위에 `@deco` 를 추가로 적었다. func() 만을 실행했을 뿐인데 위에서 선언해둔 deco 함수가 실행됐다.

	>>> @deco
	... def func():  # 목적 함수
	...     print('칼을 휘둘러 데미지 30을 주었다!!')
	... 
	>>> func()
	칼을 휘둘러 데미지 30을 주었다!!
	불 속성 데미지 15를 추가로 주었다!!

> #### 여기서 잠깐!
> 
> 발췌 - coreapython
>
>> ##### 장식자 함수는 함수를 돌려주는가?
>> 아니다. 장식자 함수는 절대로 무엇이든 돌려줄 수 있으며, 파이썬은 목표 함수를 그 반환 값으로 교체한다. 예를 들어, 다음과 같이 할 수도 있다
>> 
	def decorator_evil(target):
		return False  
>>
	@decorator_evil
	def target(a,b):
    	return a + b
>>
	>>> target
	False
>>
	>>> target(1,2)
	TypeError: 'bool' object is not callable```

장식자 함수는 목적 함수가 무엇을 하든 그냥 bool 형태의 False를 반환한다. 이 장식자를 이용하는 함수는 결국 함수가 아닌 bool 자료형이 되기 때문에  호출될 수 없다며 `TypeError`를 일으킨다. 함수 호출이 아닌 변수로 호출하면 target은 bool 형태의 False 값을 주게된다.

> target이 받아야 할 인자 값 없이도 장식자를 사용한 함수가 실행되는가?

장식자를 사용한다는건 결국 위의 예제는 `target = decorator_evil(target)` 과 같은 말이기 때문에 목적함수의 인자 값은 나중 이야기가 된다.

### 인자를 가지는 목적 함수
인자를 가지는 목적 함수를 위한 장식자 역시 **똑같은 인자 값을 받을 수 있도록 해 줘야 한다**. 하지만 장식자는 하나의 함수를 위해서 만들어 지지 않는다. 우리는 장식자가 목적함수의 어떤한 인자 값이라도 처리해 줄 수 있도록 **'임의의 비 키워드 인자와 키워드 인자'** 를 사용하도록 하자. - \*args, \**kwargs 참조 

#### 인자값을 가지는 장식자 함수
하나의 장식자는 서로 다른 데이터 타입의 인자를 받는 목적 함수 처리를 위하여 아래와 같이 **args, **kwargs를 사용하였다.

	import time
	
	def deco(f):
	    def new_func(*args, **kwargs):  # 추가 기능을 가진 함수 정의
	        print('[{0}] func: {1}'.format(time.asctime(), f.__name__), end= ' : ')
	        f(*args, **kwargs)
	    return new_func  # new_func 함수 이름을 반환
	
	@deco
	def func_99dan(d, n):  # 목적 함수, 정수형 인자 두 개
	    print('{0} X {1} = {2}'.format(d, n, d*n))
	
	@deco
	def func_invitation(info): # 목적 함수, 사전형 인자 한 개
	    print('안녕하세요. {name}님, {age}번째 생일을 축하합니다.'.format_map(info))
	
	
	func_99dan(2,5)
	func_invitation({'name':'임덕규', 'age':33})
	
결과 값

	[Tue Sep  8 03:55:04 2015] func: func_99dan : 2 X 5 = 10
	[Tue Sep  8 03:55:04 2015] func: func_invitation : 안녕하세요. 임덕규님, 33번째 생일을 축하합니다.
	
인자 값을 가진 장식자 함수를 위 예제에 맞춰 풀어서 보면  `func_99dan = func_99dan = deco(func_99dan)(2, 5)` 와 같은 같은 모양과 같다.

### inspect 함수를 이용하여 인자 값들을 사전 형태로 받기
이제는 장식자가 다양한 데이터 타입의 인자를 받기 때문에 자료형을 항상 검사해야만 했다. 아래의 예제는 실인수 데이터가 예상밖의 형태로 들어올 때 일어날 수 있는 에러를 재현해 보았다.

	def deco(f):
	    def new_func(*args, **kwargs):
	        print('arg[0] : ', args[0])
	        print("kwargs.get('n') : ", kwargs.get('n'))
	    return new_func
	
	@deco
	def target(n):
	    pass
	
	target(100)  # args 에 튜플형으로 넘어간다
	target(n=100)  # kwargs 에 사전형으로 넘어간다.
	
목적 함수는 데이터를 n 이라는 **가인수명**을  통해 넘기게 된다. 이름을 명시해주지 않고 넘긴 첫 번째 호출은 **다행히** args에 들어가 있기 때문에 첫 번째 target 호출에서는 에러가 나지 않는다. 하지만 문제는 두 번째 `target(n=100)` 에서 일어난다.

	Traceback (most recent call last):
	arg[0] :  100
	  File "/Users/raven/Desktop/python_study/deco2.py", line 15, in <module>
	kwargs.get('n') :  None
	    target(n=100)
	  File "/Users/raven/Desktop/python_study/deco2.py", line 6, in new_func
	    print('arg[0] : ', args[0])
	IndexError: tuple index out of range

억지로 호출하였던 args의 0번 인덱스를 호출하다가 `IndexError`를 일으켰다. 에러를 일으키기 위한 코드이긴 했지만, 인수 호출에 자유로운 장식자를 만들기 위해선 방법을 바꾸어야 한다.

#### inspect 함수 사용
inspect 함수는 그 이름처럼 함수를 검사하여 원하는 정보를 뽑을 수 있다.

	import inspect
	
	def deco(f):
	    def new_func(*args, **kwargs):
	        f_args = inspect.getcallargs(f, *args, **kwargs)  # 인수를 모두 사전형으로 반환
	        print(f_args['n'])  # 사전 키 값을 이용
	    return new_func
	
	@deco
	def target(n):
	    pass
	
	target(100)
	target(n=100)

inspect.getcallargs() 에 검사할 함수 이름과 가변형 인수들을 넣어주면 인수들을 함수가 호출될때 받았던 가인수명을 key 이름으로 가진 사전형 데이터로 변환해 준다.

	100
	100

---

## 목적 함수의 속성 보존하기
장식자는 목적 함수를 이용하여 **새로운** 함수를 만들어서 반환한다. 새로운 함수는 목적함수가 가지고 있던 속성값이 다르거나 없다. **functools** 모듈의 **wraps** 장식자를 이용하면 이런 문제를 해결할 수 있다.

### 장식자 사용전의 target() 함수의 속성

	def deco(f):
	    def new_func(*args, **kwargs):
	        f(*args, **kwargs)
	    return new_func
	
	def target():
	    '''
	    타겟 함수입니다.
	    '''
	    pass
	    
	print(target.__doc__)
	print(target.__name__)

결과 값은 우리의 예상대로 target함수가 가진 속성 값이 나온다.

    	타겟 함수입니다.
    
	target

### 장식자 사용후의 target() 함수의 속성
	
	@deco
	def target():
	    '''
	    타겟 함수입니다.
	    '''
	    pass
	
	print(target.__doc__)
	print(target.__name__)

new_func로 함수가 대체되었기 때문에 doc 속성값은 없으며, \_\_name\_\_은 **new_func** 함수 이름을 반환한다.

	None
	new_func

### functools 모듈의 wraps 장식자를 이용하여 보존하기
functools 의 wraps함수는 update_wrapper를 사용하기 편하게 장식자로 만들어둔 함수이다.

	import functools
	
	def deco(f):
	    @functools.wraps(f)
	    def new_func(*args, **kwargs):
	        pass
	    return new_func
		
	@deco
	def target():
	    '''
	    타겟 함수입니다.
	    '''
	    pass
	
	print(target.__doc__)
	print(target.__name__)

functools를 import 한다. 장식자 deco의 new_func 함수를 장식해야 한다. 

	    타겟 함수입니다.
    
	target

---

## 장식자 중첩 사용
만들어둔 여러개의 장식자를 하나의 목적 함수에 적용시킬 수 있다. 그렇다면 중첩 장식자 은 어떤 순서로 적용되며 어떻게 사용할 수 있는지 알아보자.

### 장식자 중첩자 순서
목적 함수에 가장 가깝게 **장식** 된 순서로 적용된다. 아래 예제는 어떠한 문자열을 받는다. 장식자를 통해서 문자열에 itelic과 bold TAG로 감싸는 코드이다. 감싸지는 순서를 잘 살표보자.

	def itelic(f):
	    def new_func(*args, **kwargs):
	        return'{0}{1}{2}'.format('<i>', f(*args, **kwargs), '</i>')
	    return new_func
	
	def bold(f):
	    def new_func(*args, **kwargs):
	        return'{0}{1}{2}'.format('<b>', f(*args, **kwargs), '</b>')
	    return new_func
	
	
	@bold
	@itelic
	def target(data):
	    return data

결과는 목적 함수에 가깝게 있던 장식자 순으로 적용되었다.

	<b><i>hello world</i></b>

이 코드는 `bold(itelic(target(data)))` 과 같다고 볼 수 있다.

## 참고 사이트
* [PEP 0318](https://www.python.org/dev/peps/pep-0318/)
* [채문창님 블로그](http://mcchae.egloos.com/11030528)
* [WireFrame](http://soooprmx.com/wp/archives/3999)
* [서광열의 프로그래밍 이야기](http://skyul.tistory.com/206)
* [CoreaPython](http://coreapython.hosting.paran.com/tiphack/Python%20Decorators%20Don't%20Have%20to%20be%20(that)%20Scary%20-%20Siafoo.htm)
* [Python Tips, Tricks, and Hacks](http://www.siafoo.net/article/52#arbitrary-numbers-of-arguments)
* 파이썬 바이블 3 - 이강성 저, 프리렉
* 실전 파이썬 프로그래밍 - 줄리안 단주 지음, 김용후 옮김, 인사이트




