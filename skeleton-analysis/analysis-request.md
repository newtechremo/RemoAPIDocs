---
description: 이미지에 있는 측정 대상의 골격(skeleton)을 분석하는 API입니다.
---

# 이미지 골격 분석 요청

## 이미지 골격 분석 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-skeleton`

사진(front, side)과 키(height), 몸무게(weight), 나이(age), 성별(gender), 생년월일(birthday)를 입력 받아 신체 골격을 분석합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>Email</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>UserKey</code></td><td>string</td><td>발급 받은 유저 키 값</td><td>true</td></tr><tr><td><code>APIKey</code></td><td>string</td><td>발급 받은 API 키 값</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>task uuid</td><td>true</td></tr><tr><td><code>forigimg</code></td><td>string(base64)</td><td>base64로 인코딩 된 정면 사진</td><td>true</td></tr><tr><td><code>sorigimg</code></td><td>string(base64)</td><td>base64로 인코딩 된 측면 사진</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="255">Name</th><th width="94">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>uuid</code></td><td>string</td><td>파라미터로 전달 받은 uuid</td></tr><tr><td><code>forigimg</code></td><td>string</td><td>정면 사진에 결과를 그려 base64로 인코딩된 이미지</td></tr><tr><td><code>sorigimg</code></td><td>string</td><td>측면 사진에 결과를 그려 base64로 인코딩된 이미지</td></tr><tr><td><code>data</code></td><td>dict</td><td>결과 dictionary</td></tr><tr><td><code>state</code></td><td>int</td><td>성공 시 0, 실패 시 -1</td></tr><tr><td><code>far_coords</code></td><td>string</td><td>json string으로 변환된 정면 2D keypoint</td></tr><tr><td><code>side_part</code></td><td>float</td><td>측면 사진의 사람이 어느 방향으로 서있는지. 0보다 작으면 왼쪽, 크면 오른쪽.</td></tr><tr><td><code>sar_coords</code></td><td>string</td><td>json string으로 변환된 측면 2D keypoint</td></tr><tr><td><code>far_head_bal_m_</code></td><td>int</td><td>머리 균형도(머리 기울기)</td></tr><tr><td><code>far_pelvic_bal_m_</code></td><td>int</td><td>골반 균형도(골반 기울기)</td></tr><tr><td><code>far_shoulder_bal_m_</code></td><td>int</td><td>어깨 균형도(어깨 기울기)</td></tr><tr><td><code>far_left_qang_m_</code></td><td>int</td><td>왼쪽 오다리값</td></tr><tr><td><code>far_right_qang_m_</code></td><td>int</td><td>오른쪽 오다리 값</td></tr><tr><td><code>far_knee_bal_m_</code></td><td>int</td><td>무릎 균형도(무릎 기울기)</td></tr><tr><td><code>far_tilt_m_</code></td><td>int</td><td>정면 축 기울기(좌우 기울기)</td></tr><tr><td><code>turtle_neck_m_</code></td><td>int</td><td>거북목 기울기</td></tr><tr><td><code>round_shoulder_m_</code></td><td>int</td><td>굽은 어께 기울기</td></tr><tr><td><code>sar_tilt_m_</code></td><td>int</td><td>측면 기울기(앞뒤 기울기)</td></tr><tr><td><code>sar_head_tilt_m_</code></td><td>int</td><td>측면 머리 균형도(측면 머리 기울기)</td></tr></tbody></table>

**요청 예시**

```json
{
  "Email": “example@email.com”,
  "UserKey": “userkey”,
  "APIKey": “apikey”,
  "uuid": “55f75582-2c4d-4bd9-9e03-9b75f7bc3058”,
  "forigimg": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBw ... (생략)(이미지를 바이트로 변환한 결과)",
  "sorigimg": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBw ... (생략)(이미지를 바이트로 변환한 결과)"
 }
```

**예시 코드**

{% tabs %}
{% tab title="curl" %}
```bash
curl -X POST "http://api.remo.re.kr/api/analysis-skeleton" \
-H "Content-Type: application/json" \
-d '{
    "Email": "your_email",
    "UserKey": "your_user_key",
    "APIKey": "your_api_key",
    "uuid": "'$(uuidgen)'",
    "forigimg": "'$(base64 -w 0 path/to/your/front/image)'",
    "sorigimg": "'$(base64 -w 0 path/to/your/side/image)'"
}'
```
{% endtab %}

{% tab title="Python" %}
```python
import requests
import uuid
import base64

fimg_path = "path/to/your/front/image"
simg_path = "path/to/your/side/image"

with open(fimg_path, "rb") as img_file:
    fimg_b64 = base64.b64encode(img_file.read()).decode('utf-8')
with open(simg_path, "rb") as img_file:
    simg_b64 = base64.b64encode(img_file.read()).decode('utf-8')

task_uuid = str(uuid.uuid4())
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", 'uuid': task_uuid, "forigimg": fimg_b64, "sorigimg": simg_b64}

res = requests.post("http://api.remo.re.kr/api/analysis-skeleton", json=rq_dict)
```
{% endtab %}

{% tab title="javascript" %}
```javascript
import fetch from 'node-fetch';
import fs from 'fs';
import { v4 as uuidv4 } from 'uuid';

const fimg_path = "path/to/your/front/image";
const simg_path = "path/to/your/side/image";

const fimg_b64 = fs.readFileSync(fimg_path, { encoding: 'base64' });
const simg_b64 = fs.readFileSync(simg_path, { encoding: 'base64' });

const task_uuid = uuidv4();
const rq_dict = {
  Email: "your_email",
  UserKey: "your_user_key",
  APIKey: "your_api_key",
  uuid: task_uuid,
  forigimg: fimg_b64,
  sorigimg: simg_b64
};

fetch("http://api.remo.re.kr/api/analysis-skeleton", {
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
  "state": 0,
  "far_coords": "[[1152, 1085], [1162, 1371], [1015, 1418], [820, 1666], [682, 1871], [1308, 1426], [1523, 1683], [1672, 1894], [1019, 1888], [989, 2376], [981, 2710], [1264, 1899], [1263, 2386], [1255, 2718], [1138, 1894], [1151, 1649], [1160, 1274], [1236, 1211], [1192, 1156], [1156, 1193], [1077, 1215], [1118, 1159]]",
  "side_part": 170.0999755859375,
  "sar_coords": "[[1200, 1111], [1182, 1388], [1179, 1436], [1174, 1680], [1130, 1867], [1197, 1437], [1195, 1719], [1167, 1970], [1163, 1885], [1165, 2342], [1203, 2664], [1179, 1916], [1184, 2419], [1228, 2787], [1157, 1899], [1195, 1664], [1170, 1293], [1176, 1232], [1083, 1188], [1041, 1226], [1171, 1243], [1082, 1192]]",
  "far_head_bal_m_": 2721,  
  "far_pelvic_bal_m_": 113,
  "far_shoulder_bal_m_": 1,
  "far_left_qang_m_": 1701,
  "far_right_qang_m_": 502,
  "far_knee_bal_m_": -485,
  "far_tilt_m_": -869,
  "turtle_neck_m_": 30160,
  "round_shoulder_m_": 2302,
  "sar_tilt_m_": -1464,
  "sar_head_tilt_m_": -1548
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "data":
  {
  "state": -1,
  'errors': "image load error" 
  }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "data":
  {
  "state": -1,
  'message': "processing error" 
  }
}
```
{% endtab %}
{% endtabs %}
