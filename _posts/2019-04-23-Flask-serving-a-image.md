---
layout: article
title: Flask 이미지 파일 요청 처리
aside:
  toc: true
tags: ["Python", "Flask"]
---

{% highlight python linenos %}

# flask-restplus 이용
# 화면 전체 스크린샷을 찍어서 전송하는 예제

from PIL import ImageGrab
from flask_restplus import Resource

class PamRequestScreenShot(Resource):
    """
    현재 화면을 캡쳐하여 반환
    """
    def get(self):
        img = ImageGrab.grab()
        buffer = io.BytesIO()
        img.save(buffer, 'PNG')
        buffer.seek(0)
        return send_file(
            buffer, attachment_filename='a.png', mimetype='image/png')
            
{% endhighlight %}
	