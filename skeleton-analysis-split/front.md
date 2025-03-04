---
description: 정면 이미지에 있는 측정 대상의 골격(skeleton)을 분석하는 API입니다.
---

# 정면 이미지 골격 분석 요청

### 정면 이미지 골격 분석 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-skeleton-v2-front`

정면 사진을 입력 받아 신체 골격을 분석합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>Email</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>UserKey</code></td><td>string</td><td>발급 받은 유저 키 값</td><td>true</td></tr><tr><td><code>APIKey</code></td><td>string</td><td>발급 받은 API 키 값</td><td>true</td></tr><tr><td><code>forigimg</code></td><td>string(base64)</td><td>base64로 인코딩 된 정면 사진</td><td>true</td></tr></tbody></table>

**응답(json)**

\*왼쪽 오른쪽 기준은 사진의 피사체 기준

<table><thead><tr><th width="282">Name</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>state</code></td><td>bool</td><td>성공 시 True, 실패 시 False</td></tr><tr><td><code>status_code</code></td><td>int</td><td>성공 시 200, 실패 시 에러 코드값 전달</td></tr><tr><td><code>uuid</code></td><td>string</td><td>파라미터로 전달 받은 uuid</td></tr><tr><td><code>credit_change</code></td><td>int</td><td>분석에서 사용된 크레딧 수량</td></tr><tr><td><code>credit</code></td><td>int</td><td>현재 소지한 크레딧</td></tr><tr><td><code>forigimg</code></td><td>string</td><td>정면 사진에 결과를 그려 base64로 인코딩된 이미지</td></tr><tr><td><code>far_coords</code></td><td>string</td><td>json 문자열로 변환된 정면 2차원 골격 좌표</td></tr><tr><td><code>far_head_bal_m_</code></td><td>float</td><td>머리 균형도(머리 기울기). degree 단위.</td></tr><tr><td><code>far_head_bal_grade</code></td><td>int</td><td><p>머리 균형도(머리 기울기).</p><p>-2 : 오른쪽 위로 기울어짐 위험(value&#x3C;=-4)</p><p>-1 : 오른쪽 위로 기울어짐 주의(-4&#x3C;value&#x3C;=-1)</p><p>0 : 정상(-1&#x3C;value&#x3C;1)</p><p>1 : 왼쪽 위로 기울어짐 주의(1&#x3C;=value&#x3C;4)</p><p>2 : 왼쪽 위로 기울어짐 위험(value>=4)</p></td></tr><tr><td><code>far_pelvic_bal_m_</code></td><td>float</td><td>골반 균형도(골반 기울기). degree 단위.</td></tr><tr><td><code>far_pelvic_bal_grade</code></td><td>int</td><td><p>골반 균형도(골반 기울기).<br>-2 : 오른쪽 위로 기울어짐 위험(value&#x3C;=-4)</p><p>-1 : 오른쪽 위로 기울어짐 주의(-4&#x3C;value&#x3C;=-1)</p><p>0 : 정상(-1&#x3C;value&#x3C;1)</p><p>1 : 왼쪽 위로 기울어짐 주의(1&#x3C;=value&#x3C;4)</p><p>2 : 왼쪽 위로 기울어짐 위험(value>=4)</p></td></tr><tr><td><code>far_shoulder_bal_m_</code></td><td>float</td><td>어깨 균형도(어깨 기울기). degree 단위.</td></tr><tr><td><code>far_shoulder_bal_grade</code></td><td>int</td><td><p>어깨 균형도(어깨 기울기).<br>-2 : 오른쪽 위로 기울어짐 위험(value&#x3C;=-4)</p><p>-1 : 오른쪽 위로 기울어짐 주의(-4&#x3C;value&#x3C;=-1)</p><p>0 : 정상(-1&#x3C;value&#x3C;1)</p><p>1 : 왼쪽 위로 기울어짐 주의(1&#x3C;=value&#x3C;4)</p><p>2 : 왼쪽 위로 기울어짐 위험(value>=4)</p></td></tr><tr><td><code>far_left_qang_m_</code></td><td>float</td><td>왼쪽 오다리 값. degree 단위.</td></tr><tr><td><code>far_left_qang_grade</code></td><td>int</td><td><p>왼쪽 오다리 값 평가.<br>-2 : X다리 위험(value&#x3C;=-12)</p><p>-1 : X다리 주의(-12&#x3C;value&#x3C;=-6)</p><p>0 : 정상(-6&#x3C;value&#x3C;6)</p><p>1 : O다리 주의(6&#x3C;=value&#x3C;12)</p><p>2 : O다리 위험(value>=12)</p></td></tr><tr><td><code>far_right_qang_m_</code></td><td>float</td><td>오른쪽 오다리 값. degree 단위.</td></tr><tr><td><code>far_right_qang_grade</code></td><td>int</td><td><p>오른쪽 오다리 값 평가.<br>-2 : X다리 위험(value&#x3C;=-12)</p><p>-1 : X다리 주의(-12&#x3C;value&#x3C;=-6)</p><p>0 : 정상(-6&#x3C;value&#x3C;6)</p><p>1 : O다리 주의(6&#x3C;=value&#x3C;12)</p><p>2 : O다리 위험(value>=12)</p></td></tr><tr><td><code>far_knee_bal_m_</code></td><td>float</td><td>무릎 균형도(무릎 기울기). degree 단위.</td></tr><tr><td><code>far_knee_bal_grade</code></td><td>int</td><td><p>무릎 균형도(무릎 기울기) 평가.<br>-2 : 오른쪽 위로 기울어짐 위험(value&#x3C;=-4)</p><p>-1 : 오른쪽 위로 기울어짐 주의(-4&#x3C;value&#x3C;=-1)</p><p>0 : 정상(-1&#x3C;value&#x3C;1)</p><p>1 : 왼쪽 위로 기울어짐 주의(1&#x3C;=value&#x3C;4)</p><p>2 : 왼쪽 위로 기울어짐 위험(value>=4)</p></td></tr><tr><td><code>far_tilt_m_</code></td><td>float</td><td>정면 축 기울기(좌우 기울기). degree 단위.</td></tr><tr><td><code>far_tilt_grade</code></td><td>int</td><td><p>정면 축 기울기(좌우 기울기) 평가.<br>-2 : 오른쪽 위로 기울어짐 위험(value&#x3C;=-4)</p><p>-1 : 오른쪽 위로 기울어짐 주의(-4&#x3C;value&#x3C;=-1)</p><p>0 : 정상(-1&#x3C;value&#x3C;1)</p><p>1 : 왼쪽 위로 기울어짐 주의(1&#x3C;=value&#x3C;4)</p><p>2 : 왼쪽 위로 기울어짐 위험(value>=4)</p></td></tr></tbody></table>

**요청 예시**

```json
{
  "Email": “example@email.com”,
  "UserKey": “userkey”,
  "APIKey": “apikey”,
  "forigimg": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBw ... (생략)(이미지를 바이트로 변환한 결과)"
 }
```

**예시 코드**

{% tabs %}
{% tab title="curl" %}
```bash
curl -X POST "http://api.remo.re.kr/api/analysis-skeleton-v2-front" \
-H "Content-Type: application/json" \
-d '{
    "Email": "your_email",
    "UserKey": "your_user_key",
    "APIKey": "your_api_key",
    "forigimg": "'$(base64 -w 0 path/to/your/front/image)'"
}'
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
import uuid
import base64

fimg_path = "path/to/your/front/image"

with open(fimg_path, "rb") as img_file:
    fimg_b64 = base64.b64encode(img_file.read()).decode('utf-8')

task_uuid = str(uuid.uuid4())
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", "forigimg": fimg_b64}

res = requests.post("http://api.remo.re.kr/api/analysis-skeleton-v2-front", json=rq_dict)
```
{% endtab %}

{% tab title="javascript" %}
```javascript
import fetch from 'node-fetch';
import fs from 'fs';
import { v4 as uuidv4 } from 'uuid';

const fimg_path = "path/to/your/front/image";

const fimg_b64 = fs.readFileSync(fimg_path, { encoding: 'base64' });

const task_uuid = uuidv4();
const rq_dict = {
  Email: "your_email",
  UserKey: "your_user_key",
  APIKey: "your_api_key",
  forigimg: fimg_b64
};

fetch("http://api.remo.re.kr/api/analysis-skeleton-v2-front", {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(rq_dict)
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));

```
{% endtab %}
{% endtabs %}

**응답 예시**

{% tabs %}
{% tab title="200" %}
```json
{
  'state': True,
  'status_code': 200,
  'APIName': 'Analysis-skeleton-v2-front',
  'credit_change': -1,
  'credit': 99984228,
  'uuid': '59e9a3a1-a8d2-42a1-b2af-3a87cd01f682',
  'forigimg': 'data:image/jpeg;base64,/9j/4A ... (중략) ... A8x//2Q==',
  'far_coords': '[[431, 258], [432, 403], [360, 432], [301, 595], [246, 720], [505, 434], [566, 598], [621, 723], [370, 675], [387, 953], [392, 1151], [499, 674], [485, 951], [473, 1152], [435, 676], [432, 545], [432, 356], [472, 328], [452, 304], [433, 329], [391, 328], [413, 308]]',
  'far_head_bal_grade': 1,
  'far_head_bal_m_': 1.393,
  'far_knee_bal_grade': 0,
  'far_knee_bal_m_': 0.57,
  'far_left_qang_grade': 0,
  'far_left_qang_m_': -2.529,
  'far_pelvic_bal_grade': 1,
  'far_pelvic_bal_m_': 1.153,
  'far_right_qang_grade': 0,
  'far_right_qang_m_': -4.368,
  'far_shoulder_bal_grade': 0,
  'far_shoulder_bal_m_': 0.483,
  'far_tilt_grade': 0,
  'far_tilt_m_': 0.958,
}
```
{% endtab %}

{% tab title="400 ~" %}
```json
{
  "state": False,
  "credit": 100,
  "message": 'error from front image decoding b64',
  "status":413
}
```
{% endtab %}

{% tab title="500 ~" %}
```json
{
  "state": False,
  "credit": 100,
  "message": 'In the front image, the model is not facing side ',
  "status": 515
}
```
{% endtab %}
{% endtabs %}

**에러 코드 안내**

| 대분류          | 소분류                   | 코드  |
| ------------ | --------------------- | --- |
| 입력 데이터 문제 발생 | 프로토콜 에러               | 400 |
|              | 입력 데이터 없음             | 411 |
|              | 첨부 이미지 에러             | 412 |
|              | 첨부 이미지 에러(정면)         | 413 |
|              | 사진이 10도 초과 기울어 있음(정면) | 418 |
| 기타 이슈 발생     | 사용 유저 확인 안됨           | 420 |
|              | APIKey 틀림             | 421 |
|              | 크리딧 부족                | 422 |
| 분석 이슈 발생     | 정면 사진 사람 인식 안됨        | 511 |
|              | 정면 사진의 각도 틀림          | 514 |
|              | 정면 이미지의 A자 포즈 아님      | 517 |
| 프로세스 에러      | 프로세스 처리 에러            | 550 |
|              | 프로세스 처리 기타 에러         | 559 |

**요청 이미지 결과 보기**

{% tabs %}
{% tab title="Python" %}
```python
import requests
import uuid
import base64
import cv2
import numpy as np
import uuid

fimg_path = "path/to/your/front/image"

with open(fimg_path, "rb") as img_file:
    fimg_b64 = base64.b64encode(img_file.read()).decode('utf-8')

task_uuid = str(uuid.uuid4())
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", 'uuid': task_uuid, "forigimg": fimg_b64}
res = requests.post("http://api.remo.re.kr/api/analysis-skeleton-v2-front", json=rq_dict).json()

fimg_b64 = res["forigimg"] 
f_bytes = base64.b64decode(split_b64_video(fimg_b64).encode('utf-8'))
front_nparr = np.frombuffer(f_bytes, np.uint8)
front_img = cv2.imdecode(front_nparr, cv2.IMREAD_COLOR)

cv2.imshow('front_img', front_img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
{% endtab %}
{% endtabs %}

**결과 이미지**

<figure><img src="../.gitbook/assets/forig.jpg" alt="" width="375"><figcaption><p>forigimg</p></figcaption></figure>
