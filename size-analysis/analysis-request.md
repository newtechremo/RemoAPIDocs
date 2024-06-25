---
description: 이미지에 있는 측정 대상의 체형과 신체 치수를 분석하는 API입니다.
---

# 이미지 체형 치수 분석 요청

## 이미지 체형 치수 분석 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-shape`

사진(front, side)과 키(height), 몸무게(weight), 나이(age), 성별(gender), 생년월일(birthday)를 입력 받아 신체 체형과 치수를 측정합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>Email</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>UserKey</code></td><td>string</td><td>발급 받은 유저 키 값</td><td>true</td></tr><tr><td><code>APIKey</code></td><td>string</td><td>발급 받은 API 키 값</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>task uuid</td><td>true</td></tr><tr><td><code>forigimg</code></td><td>string(base64)</td><td>base64로 인코딩 된 정면 사진</td><td>true</td></tr><tr><td><code>sorigimg</code></td><td>string(base64)</td><td>base64로 인코딩 된 측면 사진</td><td>true</td></tr><tr><td><code>gender</code></td><td>int</td><td>성별(남자:1, 여자:2)</td><td>true</td></tr><tr><td><code>height_mm</code></td><td>int</td><td>분석 대상의 키(mm 단위)</td><td>true</td></tr><tr><td><code>weight_g</code></td><td>int</td><td>분석 대상의 몸무게(g 단위)</td><td>true</td></tr><tr><td><code>age</code></td><td>int</td><td>분석 대상의 나이</td><td>true</td></tr><tr><td><code>birthday</code></td><td>string</td><td>분석 대상의 생년월일 8글자</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="167">Name</th><th width="88">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>data</code></td><td>dict</td><td>결과 dictionary</td></tr><tr><td><code>state</code></td><td>int</td><td>성공 시 0, 실패 시 -1</td></tr><tr><td><code>errors</code></td><td>string</td><td>에러가 발생한 경우 에러메세지 전달</td></tr><tr><td><code>message</code></td><td>string</td><td>처리 관련 안내 메시지</td></tr><tr><td><code>shape_class</code></td><td>int</td><td>0: 사각형, 1: 둥근형, 2: 삼각형, 3: 역삼각형, 4: 모래시계형</td></tr><tr><td><code>shape_size</code></td><td>int</td><td>0 ~ 4까지 값으로 구성. 0 매우 마름, 1: 마름, 2:표준, 3: 과체중, 4: 비만</td></tr><tr><td><code>chest</code></td><td>int</td><td>mm 단위, 가슴 둘레</td></tr><tr><td><code>chest_max</code></td><td>int</td><td>mm 단위, 가슴 최대 둘레</td></tr><tr><td><code>chest_min</code></td><td>int</td><td>mm 단위, 가슴 최소 둘레</td></tr><tr><td><code>chest_per</code></td><td>int</td><td>% 단위</td></tr><tr><td><code>height_per</code></td><td>int</td><td>% 단위</td></tr><tr><td><code>hip</code></td><td>int</td><td>mm 단위, 엉덩이 둘레</td></tr><tr><td><code>hip_max</code></td><td>int</td><td>mm 단위, 엉덩이 최대 둘레</td></tr><tr><td><code>hip_min</code></td><td>int</td><td>mm 단위, 엉덩이 최소 둘레</td></tr></tbody></table>

**요청 예시**

```json
{
  "Email": “your_email”,
  "UserKey": “your_user_key”,
  "APIKey": “your_api_key”,
  "uuid": “55f75582-2c4d-4bd9-9e03-9b75f7bc3058”,
  "forigimg": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBw ... (생략)(이미지를 바이트로 변환한 결과)",
  "sorigimg": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBw ... (생략)(이미지를 바이트로 변환한 결과)"
  "gender": 2,
  "height_mm": 1650,
  "weight_g": 65000,
  "age": 100,
  "birthday": “20101010”
 }
```

**예시 코드**

{% tabs %}
{% tab title="curl" %}
```bash
curl -X POST "http://api.remo.re.kr/api/analysis-shape" \
-H "Content-Type: application/json" \
-d '{
    "Email": "your_email",
    "UserKey": "your_user_key",
    "APIKey": "your_api_key",
    "uuid": "'$(uuidgen)'",
    "forigimg": "'$(base64 -w 0 path/to/your/front/image)'",
    "sorigimg": "'$(base64 -w 0 path/to/your/side/image)'",
    "gender": 2,
    "height_mm": 1650,
    "weight_g": 65000,
    "age": 15,
    "birthday": "20101010"
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
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", 'uuid': task_uuid, "forigimg": fimg_b64, "sorigimg": simg_b64, "gender": 2, "height_mm": 1650, "weight_g": 65000, "age": 15, "birthday": "20101010"}

res = requests.post("http://api.remo.re.kr/api/analysis-shape", json=rq_dict)
```
{% endtab %}

{% tab title="javascript" %}
```javascript
import fetch from 'node-fetch';
import fs from 'fs';
import { v4 as uuidv4 } from 'uuid';

const fimg_path = "path/to/your/front/image";
const simg_path = "path/to/your/side/image";

const fimg_b64 = fs.readFileSync(fimg_path, 'base64');
const simg_b64 = fs.readFileSync(simg_path, 'base64');

const task_uuid = uuidv4();
const rq_dict = {
  Email: "your_email",
  UserKey: "your_user_key",
  APIKey: "your_api_key",
  uuid: task_uuid,
  forigimg: fimg_b64,
  sorigimg: simg_b64,
  gender: 2,
  height_mm: 1650,
  weight_g: 65000,
  age: 15,
  birthday: "20101010"
};

fetch("http://api.remo.re.kr/api/analysis-shape", {
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
  "data": {
    "chest": 894,
    "chest_max": 897,
    "chest_min": 856,
    "chest_per": 23,
    "height_per": 99,
    "hip": 931,
    "hip_max": 943,
    "hip_min": 848,
    "hip_per": 54,
    "message": "processing done",
    "shape_class": 0,
    "state": 0,
    "thigh": 526,
    "thigh_max": 531,
    "thigh_min": 434,
    "thigh_per": 87,
    "waist": 730,
    "waist_max": 746,
    "waist_min": 722,
    "waist_per": 2,
    "weight_per": 78,
    “left_up_arm_length”: 18.948232737856337,
    “right_up_arm_length”: 17.85270382242535,
    “left_down_arm_length”: 18.1537781560452,
    “right_down_arm_length”: 17.529966293677035,
    “left_arm_length”: 37.102010893901536,
    “right_arm_length”: 35.38267011610238,
   “left_up_leg_length”: 26.49846457688673,
   “right_up_leg_length”: 25.853059057438635,
   “left_down_leg_length”: 32.56943512408277,
   “right_down_leg_length”: 28.074971378799322,
   “left_leg_length”: 59.067899700969505,
   “right_leg_length”: 53.928030436237954,
   “lower_body_length”: 45.217383771616056,
   “trunk_length”: 31.456454492717803,
   “head_length”: 21.271475328601596,
   “body_length”: 99.99999999999999
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
