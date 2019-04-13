---
layout: article
title: 명령어를 이용하여 X 윈도우 창 선택
aside:
  toc: true
tags: ["linux"]
---


{% highlight bash linenos %}
# 창을 클릭하여 PID 찾기
$ xprop _NET_WM_PID | cut -d' ' -f3

# 창 이름을 이용하여 선택
$ wmctrl -a "Mozilla Firefox"

# 정규식을 이용하여 선택
$ wmctrl -Fa "$(wmctrl -l | sed -rn 's/^([^ ]+ +){3}(.*Mozilla Firefox)$/\2/p')"
 
# PID 를 이용하여 선택
$ wmctrl -ia $(wmctrl -lp | awk -vpid=$PID '$3==pid {print $1; exit}') 


{% endhighlight %}


