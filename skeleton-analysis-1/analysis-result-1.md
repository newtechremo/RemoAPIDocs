---
description: 완료된 골프 분석 결과를 요청하는 API입니다.
---

# 골프 분석 점수 요청

## 골프 분석 점수요청

<mark style="color:red;">`GET`</mark> `http://115.94.164.253:15003/golf/get-score/{id}/{uuid}`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 골프분석 점수 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="185">Category</th><th width="126">Name</th><th width="86">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>address</code></td><td><code>stance</code></td><td>float</td><td>스탠스 폭. 만점 40점.</td></tr><tr><td></td><td><code>upper_body_tilt</code></td><td>float</td><td>상체 기울임 정도. 만점 40점.</td></tr><tr><td></td><td><code>shoulder_tilt</code></td><td>float</td><td>어깨 기울임 정도. 만점 20점.</td></tr><tr><td><code>takeback</code></td><td><code>left_shoulder_rotation</code></td><td>float</td><td>왼쪽 어깨 회전.</td></tr><tr><td></td><td><code>right_hip_rotation</code></td><td>float</td><td>우측 골반 회전.</td></tr><tr><td></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. 만점 20점.</td></tr><tr><td></td><td><code>right_arm_flexion</code></td><td>float</td><td>오른팔 펴짐 각도. 만점 20점.</td></tr><tr><td><code>backswing</code></td><td><code>head_location</code></td><td>float</td><td>머리 위치. 만점 30점.</td></tr><tr><td></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. 만점 20점.</td></tr><tr><td></td><td><code>left_shoulder_rotation</code></td><td>float</td><td>왼쪽 어깨 회전.</td></tr><tr><td><code>backswingtop</code></td><td><code>reverse_spine</code></td><td>float</td><td>리버스 스파인. 만점 50점.</td></tr><tr><td></td><td><code>right_leg_flexion</code></td><td>float</td><td>오른 다리 펴짐 각도. 만점 10점.</td></tr><tr><td></td><td><code>head_location</code></td><td>float</td><td>머리 위치. 만점 10점.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. 만점 10점.</td></tr><tr><td></td><td><code>right_hip_rotation</code></td><td>float</td><td>우측 골반 회전.</td></tr><tr><td><code>downswing</code></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. 만점 30점.</td></tr><tr><td></td><td><code>right_elbow_location</code></td><td>float</td><td>오른팔꿈치 위치. 만점 20점.</td></tr><tr><td></td><td><code>right_arm_rotation</code></td><td>float</td><td>오른팔-겨드랑이 각도. 만점 50점.</td></tr><tr><td><code>impact</code></td><td><code>head_location</code></td><td>float</td><td>머리 위치. 만점 10점.</td></tr><tr><td></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. 만점 20점.</td></tr><tr><td></td><td><code>right_arm_flexion</code></td><td>float</td><td>오른팔 펴짐 각도. 만점 20점.</td></tr><tr><td></td><td><code>hanging_back</code></td><td>float</td><td>행잉백.</td></tr><tr><td><code>follow</code></td><td><code>left_line_align</code></td><td>float</td><td>왼쪽 라인 일직선 정도. 만점 40점.</td></tr><tr><td></td><td><code>chicken_wing</code></td><td>float</td><td>치킨윙(왼팔 펴짐 각도). 만점 20점.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. 만점 30점.</td></tr><tr><td><code>finish</code></td><td><code>left_foot_fix</code></td><td>float</td><td>왼발 고정 여부. 만점 30점.</td></tr><tr><td></td><td><code>right_foot_rotation</code></td><td>float</td><td>오른발 회전 여부. 만점 30점.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. 만점 40점.</td></tr></tbody></table>

**요청 예시**

<pre class="language-json"><code class="lang-json"><strong>http://115.94.164.253:15003/golf/get-score/example@email.com/bc692864-0243-4d41-bce3-7658c92ef0c5
</strong></code></pre>

**응답 예시**

{% tabs %}
{% tab title="200" %}
```json
{
  "address": {
    "stance": 40,
    "upper_body_tilt": 40,
    "shoulder_tilt": 4.345977503048825
  },
  "takeback": {
    "left_arm_flexion": 20,
    "right_arm_flexion": 20
  },
  "backswing": {
    "head_location": 1.5659695358451131,
    "left_arm_flexion": 20
  },
  "backswingtop": {
    "reverse_spine": 0,
    "right_leg_flexion": 0,
    "head_location": 0,
    "center_of_gravity": 0
  },
  "downswing": {
    "center_of_gravity": 20,
    "right_elbow_location": 20,
    "right_arm_rotation": 20
  },
  "impact": {
    "head_location": 8.546732188568196,
    "left_arm_flexion": 20,
    "right_arm_flexion": 0.6532090112476552
  },
  "follow": {
    "left_line_align": 6.726802145755698,
    "chicken_wing": 20,
    "center_of_gravity": 30
  },
  "finish": {
    "left_foot_fix": 0,
    "right_foot_rotation": 0,
    "center_of_gravity": 25
  }
}

```
{% endtab %}
{% endtabs %}
