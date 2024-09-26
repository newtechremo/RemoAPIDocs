---
description: 완료된 축구 분석 결과를 요청하는 API입니다.
---

# 축구 분석 점수 요청

## 축구 분석 점수요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-soccer-score`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 축구 분석 점수 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

\*항목 별 만점은 10점입니다.

<table><thead><tr><th width="126">Name</th><th width="86">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>stepping_foot_position</code></td><td>dict</td><td>디딤발 위치. 공 중심에서 발목까지 공 1.5배 거리가 이상적. 1.3 ~ 1.7 만점. 구간 전후 0.1마다 1점씩 감소.</td></tr><tr><td><code>stepping_knee_global_y</code></td><td>dict</td><td>디딤발 각도. 디딤발이 지면에서 45도 각도로 기울어져 있어야 함. 42~48 만점. 구간 전후 1마다 1점씩 감소.</td></tr><tr><td><code>stepping_knee_x</code></td><td>dict</td><td>디딤발 무릎 각도. 임팩트 시 무릎의 각도는 40~60도가 적절함. 40~60 만점. 구간 전후 1마다 1점씩 감소.</td></tr><tr><td><code>upper_pelvis_shoulder_y</code></td><td>dict</td><td>백스윙 시 골반-어깨의 y축 각도가 0보다 커야 하고, 임팩트 시에는 0보다 작아야 함. before_impact는 0보다 크고, after_impact는 0보다 작을 경우 만점. 구간을 벗어날 경우 1마다 1점씩 감소. </td></tr><tr><td><code>upper_left_shoulder_y</code></td><td>dict</td><td>백스윙 시 어깨의 y축 관절각도는 60보다 커야 하고, 임팩트 이후에는 0보다 작아야 함. before_impact는 60보다 크고, impact는 0보다 작을 경우 만점. 구간을 벗어날 경우 1마다 1점씩 감소. </td></tr><tr><td><code>upper_pelvis_shoulder_x</code></td><td>dict</td><td>임팩트 시 무게중심이 앞으로 가야 함. 이때 골반-어깨 x축 각도가 0보다 커야 함. 0보다 클 경우 만점. 구간을 벗어날 경우 1마다 1점씩 감소. </td></tr><tr><td><code>kick_right_knee_pelvis_x</code></td><td>dict</td><td>백스윙 시 차는 쪽 무릎 x축의 각도는 -90도 정도, 피니쉬 시에는 80도 정도가 적당함. before_impact는 -85~110, after_impact는 70~90 구간에 들어올 경우 만점. 구간 전후 2마다 1점씩 감소.</td></tr><tr><td><code>impact_right_knee_global_y</code></td><td>dict</td><td>임팩트 시 차는 발의 각도도 디딤발과 마찬가지로 지면과 45도 정도 되는 것이 적당함. 42~48 만점. 구간 전후 1마다 1점씩 감소.</td></tr><tr><td><code>kick_right_hip_x</code></td><td>dict</td><td>차는 발의 엉덩관절 각속도. 각속도가 빠를수록 빠른 킥임. 각속도가 170보다 크거나 같을 시 충분히 빠른 킥으로 판단하여 만점 처리. 1 벗어날 때마다 1점씩 감소.</td></tr><tr><td><code>before_impact</code></td><td>float</td><td>임팩트 시점 이전.</td></tr><tr><td><code>impact</code></td><td>float</td><td>임팩트 시점.</td></tr><tr><td><code>after_impact</code></td><td>float</td><td>임팩트 시점 이후.</td></tr></tbody></table>



**요청 예시**

```json
/analysis-soccer-score/example@email.com/bc692864-0243-4d41-bce3-7658c92ef0c5
```

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
