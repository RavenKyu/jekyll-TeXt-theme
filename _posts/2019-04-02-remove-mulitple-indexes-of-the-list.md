---
title: List 자료형에서 다수의 원소를 인덱스 목록을 이용하여 삭제
tags: [Python]
---
리스트 자료형을 다루다 보면 여러 인덱스 번호를 받아서 삭제해야 할 일이 있다.
 
사용자가 목록에서 삭제를 원하는 인덱스를 여러개 듬성듬성 지정하였을 경우, 삭제 목록을 내림차순으로 정렬하여 뒤에서 부터 삭제하면 된다.    

{% highlight python linenos %}
>>> items = ["one", "two", "three", "four"]   
>>> remove_list = [1, 3]  # 삭제 목록
>>> for index in sorted(remove_list, reverse=True):  # 삭제 목록을 내림차순으로 정렬
...    del items[index]  # 아이템 삭제
>>> print(items)
['one', 'three']
{% endhighlight %}
	





