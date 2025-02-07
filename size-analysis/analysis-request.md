---
description: API for analyzing body shape and measurements from images.
---

# Image Body Shape Analysis Request

## Image Body Shape Analysis Request

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-shape`

Measures body shape and dimensions using photos (front, side), height, weight, age, gender, and date of birth as inputs.

**Parameters(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>Email</code></td><td>string</td><td>User email address</td><td>true</td></tr><tr><td><code>UserKey</code></td><td>string</td><td>Issued user key value</td><td>true</td></tr><tr><td><code>APIKey</code></td><td>string</td><td>Issued API key value</td><td>true</td></tr><tr><td><code>forigimg</code></td><td>string(base64)</td><td>Front photo encoded in base64</td><td>true</td></tr><tr><td><code>sorigimg</code></td><td>string(base64)</td><td>Side photo encoded in base64</td><td>true</td></tr><tr><td><code>gender</code></td><td>int</td><td>Gender(Male:1, Female:2)</td><td>true</td></tr><tr><td><code>height_mm</code></td><td>int</td><td>Subject's height(in mm)</td><td>true</td></tr><tr><td><code>weight_g</code></td><td>int</td><td>Subject's weight(in g)</td><td>true</td></tr><tr><td><code>age</code></td><td>int</td><td>Subject's age</td><td>true</td></tr><tr><td><code>birthday</code></td><td>string</td><td>Subject's 8-digit date of birth</td><td>true</td></tr></tbody></table>

**Example Code**

{% tabs %}
{% tab title="curl" %}
```bash
curl -X POST "http://api.remo.re.kr/api/analysis-shape" \
-H "Content-Type: application/json" \
-d '{
    "Email": "your_email",
    "UserKey": "your_user_key",
    "APIKey": "your_api_key",
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
rq_dict = {'Email': "your_email", "UserKey": "your_user_key", "APIKey": "your_api_key", "forigimg": fimg_b64, "sorigimg": simg_b64, "gender": 2, "height_mm": 1650, "weight_g": 65000, "age": 15, "birthday": "20101010"}

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

# Response Parameters and Error Codes

**Response Parameters(json)**

<table><thead><tr><th width="173">Name</th><th width="88">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>state</code></td><td>bool</td><td>True if analysis successful, False if failed</td></tr><tr><td><code>statue_code</code></td><td>int</td><td>200 if analysis successful, refer to error code if failed</td></tr><tr><td><code>credit_change</code></td><td>int</td><td>Credits used if successful, 0 if failed</td></tr><tr><td><code>message</code></td><td>string</td><td>Request-related guidance message</td></tr><tr><td><code>shape_class</code></td><td>int</td><td>0: Rectangle, 1: Round, 2: Triangle, 3: Inverted Triangle, 4: Hourglass</td></tr><tr><td><code>shape_size</code></td><td>int</td><td>Values from 0 to 4. 0: Very Thin, 1: Thin, 2: Standard, 3: Overweight, 4: Obese</td></tr><tr><td><code>BMI</code></td><td>float</td><td>User's Body Mass Index value</td></tr><tr><td><code>WHR</code></td><td>float</td><td>User's Waist-to-Hip Ratio</td></tr><tr><td><code>height_per</code></td><td>float</td><td>Standard distribution ratio of height, median is 50(unit %)</td></tr><tr><td><code>weight_per</code></td><td>float</td><td>Standard distribution ratio of weight, median is 50(unit %)</td></tr><tr><td><code>chest</code></td><td>float</td><td>Predicted average chest circumference(unit mm)</td></tr><tr><td><code>chest_max</code></td><td>float</td><td>Predicted maximum chest circumference(unit mm)</td></tr><tr><td><code>chest_min</code></td><td>float</td><td>Predicted minimum chest circumference(unit mm)</td></tr><tr><td><code>chest_per</code></td><td>float</td><td>Standard distribution ratio of chest circumference, median is 50(unit %)</td></tr><tr><td><code>hip</code></td><td>float</td><td>Predicted average hip circumference(unit mm)</td></tr><tr><td><code>hip_max</code></td><td>float</td><td>Predicted maximum hip circumference(unit mm)</td></tr><tr><td><code>hip_min</code></td><td>float</td><td>Predicted minimum hip circumference(unit mm)</td></tr><tr><td><code>hip_per</code></td><td>float</td><td>Standard distribution ratio of hip circumference, median is 50(unit %)</td></tr><tr><td><code>waist</code></td><td>float</td><td>Predicted average waist circumference(unit mm)</td></tr><tr><td><code>waist_max</code></td><td>float</td><td>Predicted maximum waist circumference(unit mm)</td></tr><tr><td><code>waist_min</code></td><td>float</td><td>Predicted minimum waist circumference(unit mm)</td></tr><tr><td><code>waist_per</code></td><td>float</td><td>Standard distribution ratio of waist circumference, median is 50(unit %)</td></tr><tr><td><code>thigh</code></td><td>float</td><td>Predicted average thigh circumference(unit mm)</td></tr><tr><td><code>thigh_max</code></td><td>float</td><td>Predicted maximum thigh circumference(unit mm)</td></tr><tr><td><code>thigh_min</code></td><td>float</td><td>Predicted minimum thigh circumference(unit mm)</td></tr><tr><td><code>thigh_per</code></td><td>float</td><td>Standard distribution ratio of thigh circumference, median is 50(unit %)</td></tr><tr><td><code>arm_length</code></td><td>float</td><td>Average measured arm length(unit mm)</td></tr><tr><td><code>arm_per</code></td><td>float</td><td>Standard deviation of measured arm length(unit %)</td></tr><tr><td><code>leg_length</code></td><td>float</td><td>Average measured leg length(unit mm)</td></tr><tr><td><code>leg_per</code></td><td>float</td><td>Standard deviation of measured leg length(unit %)</td></tr><tr><td><code>head_length</code></td><td>float</td><td>Measured head height(unit mm)</td></tr><tr><td><code>trunk_length</code></td><td>float</td><td>Measured upper body length below head(unit mm)</td></tr><tr><td><code>lower_body_length</code></td><td>float</td><td>Measured lower body length above ankle(unit mm)</td></tr><tr><td><code>left_arm_length</code></td><td>float</td><td>Measured left arm length(mm)</td></tr><tr><td><code>left_up_arm_length</code></td><td>float</td><td>Measured left upper arm length(mm)</td></tr><tr><td><code>left_down_arm_length</code></td><td>float</td><td>Measured left forearm length(mm)</td></tr><tr><td><code>right_arm_length</code></td><td>float</td><td>Measured right arm length(mm)</td></tr><tr><td><code>right_up_arm_length</code></td><td>float</td><td>Measured right upper arm length(mm)</td></tr><tr><td><code>right_down_arm_length</code></td><td>float</td><td>Measured right forearm length(mm)</td></tr><tr><td><code>left_leg_length</code></td><td>float</td><td>Measured left leg length(mm)</td></tr><tr><td><code>left_up_leg_length</code></td><td>float</td><td>Measured left thigh length(mm)</td></tr><tr><td><code>left_down_leg_length</code></td><td>float</td><td>Measured left calf length(mm)</td></tr><tr><td><code>right_leg_length</code></td><td>float</td><td>Measured right leg length(mm)</td></tr><tr><td><code>right_up_leg_length</code></td><td>float</td><td>Measured right thigh length(mm)</td></tr><tr><td><code>right_down_leg_length</code></td><td>float</td><td>Measured right calf length(mm)</td></tr></tbody></table>

**Response Examples**

{% tabs %}
{% tab title="200" %}
```json
{
  "state": true,
  "status_code": 200,
  "APIName": "Analysis-shape",
  "credit_change": -1,
  "credit": 99,
  "uuid": "3b255cb1-ba71-4264-a52a-3bee7fe5b5c9",
  "BMI": 238.751,
  "WHR": 0.809,
  "arm_length": 527.7,
  "arm_per": 100,
  "body_length": 1650.0,
  "chest": 857.1,
  "chest_max": 859.3,
  "chest_min": 829.3,
  "chest_per": 100,
  "head_length": 265.8,
  "shape_class": 0,
  "shape_size": 2
}
```
{% endtab %}

{% tab title="400~" %}
```json
{
    "state": false,
    "status_code": 413,
    "credit_change": 0,
    "credit": 100,
    "message": "error from front image decoding b64"
}
```
{% endtab %}

{% tab title="500~" %}
```json
{
    "state": false,
    "status_code": 515,
    "credit_change": 0,
    "credit": 100,
    "message": "In the side image, the model is not facing side"
}
```
{% endtab %}
{% endtabs %}

**Error Codes**

| Category | Sub-category | Code |
|----------|-------------|------|
| Input Data Error | Protocol Error | 400 |
|  | No Input Data | 411 |
|  | Image Attachment Error | 412 |
|  | Front Image Error | 413 |
|  | Side Image Error | 414 |
|  | Input Image Upside Down (Both Front & Side) | 415 |
|  | Input Image Upside Down (Front) | 416 |
|  | Input Image Upside Down (Side) | 417 |
| Other Issues | User Not Verified | 420 |
|  | Invalid API Key | 421 |
|  | Insufficient Credits | 422 |
|  | Person Not Detected in Front Image | 511 |
|  | Person Not Detected in Side Image | 512 |
|  | Person Not Detected in Both Images | 513 |
|  | Subject Not Facing Front in Front Image | 514 |
|  | Subject Not Facing Side in Side Image | 515 |
|  | Subject Not in Correct Pose in Front/Side Images | 516 |
|  | Subject Not in A-Pose in Front Image | 517 |
|  | Subject Not in Attention Pose in Side Image | 518 |
|  | Incorrect Body Measurement Pose | 519 |