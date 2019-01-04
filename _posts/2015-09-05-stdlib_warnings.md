---
layout: article
title: "warnings - 경고를 발생시킬 수 있는 모듈"
aside:
  toc: true
tags: ["Python"]
---

## 누가, 언제, 왜 사용하나?
개발자는 **모듈 업데이트와 문서화를 할 때** 다음과 같은 목적을 가지고 사용할 수 있다. 

* 이 함수가 더는 쓰이지 않으며 **새 함수로 대체되었음을 알림** 
* 어떻게 이전 코드를 바꿀 수 있는지 **경고**

## 예제 코드
	
	import	warnings
	
	class Car(object):
		def turn_left(self):
			warnings.warn("turn_left is deprecated, use turn instead", DeprecationWarning)
			self.turn(direction='left')
		
		def turn(self, direction):
			'''차를 어떤 방향으로 회전한다.
			:param direction: 회전할 방향
			:type direction: str
			'''
			pass    		

## 유의할 점
테스트를 실행할 때 **python 인터프리터를 -W error 옵션과 함께 실행하면 경고를 '예외'로 발생시킨다.** 언젠가 중단될 함수를 호출하는 것이 에러가 되어 코드를 고쳐야 함을 정확히 알 수 있다.