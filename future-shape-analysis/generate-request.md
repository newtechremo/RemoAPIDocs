---
description: 이미지에 있는 대상의 체형 변화 시 예측 이미지를 생성하는 API입니다.
---

# 이미지 미래 체형 생성 요청

## 이미지 미래 체형 생성 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-future-shape`

대상의 사진을 받아 살이 빠진 모습과 살이 찐 모습을 생성합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>Email</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>UserKey</code></td><td>string</td><td>발급 받은 유저 키 값</td><td>true</td></tr><tr><td><code>APIKey</code></td><td>string</td><td>발급 받은 API 키 값</td><td>true</td></tr><tr><td><code>base64Image</code></td><td>string(base64)</td><td>base64로 인코딩 된  사진</td><td>true</td></tr><tr><td><code>requestMessage</code></td><td>string</td><td>“best” : 살이 빠진 모습, “worst” : 살이 찐 모습</td><td>true</td></tr><tr><td><code>gender</code></td><td>string</td><td>“male” : 남자, “female” : 여자</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="172">Name</th><th width="88">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>state</code></td><td>bool</td><td>True이면 분석 성공, False이면 분석 실패</td></tr><tr><td><code>message</code></td><td>string</td><td>분석 실패 시 문제가 발생한 부분</td></tr><tr><td><code>resultImage</code></td><td>string</td><td>결과 이미지(Base64 형식)</td></tr></tbody></table>

**예시 코드**

{% tabs %}
{% tab title="Python" %}
```python
import requests
import uuid
import base64

img_path = "path/to/your/front/image"

with open(img_path , "rb") as img_file:
    img_b64 = base64.b64encode(img_file.read()).decode('utf-8')

task_uuid = str(uuid.uuid4())
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", "base64Image": fimg_b64, "requestMessage": "best", "gender": "female"}

res = requests.post("http://api.remo.re.kr/api/analysis-shape", json=rq_dict)
```
{% endtab %}
{% endtabs %}

**요청 예시**

```json
{
    "Email": “your_email”,
    "UserKey": “your_user_key”,
    "APIKey": “your_api_key”,
    "base64Image": "AAAAIGZ0eXBpc29tAAACAGlzb21pc28yYXZjMW1wNDEAAAAIZnJlZQAK/7BtZGF0AAACugYF … (이하 생략)",
    "requestMessage": "best",
    "gender": "male"
}
```

**응답 예시**

{% tabs %}
{% tab title="200" %}
```json
{
    'state': True,
    'result_image': 'iVBORw0KGgoAAAANSUhEUgAAAgAAAAIACAIAAAB7GkOtAAAgAElEQVR4AdTBS49t23ne9//zvmPOtapq73P2uYhiFDDSoURT1AUw7VDOxTKgIBEEJTZsmvCl5e+QjoE03BEQIN9BffUFw24EBpLIUpwgaSWQaFEyFVMSEZ4rz6ldtdacY7xPag9q2bXNLQNp7t9P/83f+3u81iJtA7YB20y9d17FNq/Se2eSBEhiurm5kQToEUASj9hm0hittYioKkmZabtPmriwDSiDV7m+vu6939/f995ba9fX1xHRy+14Fbm01iIC0CMR0abMtF1Ta4eIyExJQFy01mxXlW1JEZGZEYFSUkyZqQmwHRdAXSxL+qKqfNFaO5/Pp9NpjBFTPfCgbA/bY4ze+77vvfeqkmR7TPu+96mqGn5QLwMioibbkmzXFBG2xxi2AUkRIWmMYbsmQFJEOHQ+ … (후략)'
}
```
{% endtab %}

{% tab title="400" %}
```json
{
    'state': False,
    'message': 'wrong image'
}
```
{% endtab %}

{% tab title="400" %}
```json
{
    'state': False,
    'message': 'keypoint inference error'
}
```
{% endtab %}
{% endtabs %}
