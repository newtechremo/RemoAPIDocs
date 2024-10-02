---
description: 완료된 달리기 분석 결과를 요청하는 API입니다.
---

# 달리기 분석 점수 요청

## 달리기분석 점수요청

<mark style="color:red;">`GET`</mark> `http://115.94.164.253:15003/running/get-score/{id}/{uuid}`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 달리기분석 점수 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

\*항목 별 만점은 10점입니다.

<table><thead><tr><th width="126">Name</th><th width="86">Type</th><th>Description</th></tr></thead><tbody><tr><td>right_contact</td><td>dict</td><td>오른쪽 발 컨택 시.</td></tr><tr><td>left_contact</td><td>dict</td><td>왼쪽 발 컨택 시.</td></tr><tr><td>ankle_location</td><td>list</td><td>컨택 시 발 위치는 몸 중심보다 너무 앞으로 오면 안 됨. 해당 값은 발목 위치에서 몸 중심 위치를 뺀 값. 값이 50보다 크거나 같으면 만점. 그렇지 않으면 0.1당 1점씩 차감.</td></tr><tr><td>ankle_angle</td><td>list</td><td>컨택 시 발목 각도가 0도에 가까워야 함. 값이 0~6 사이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr><tr><td>opposite_thigh_angle</td><td>list</td><td>컨택 시 반대쪽 다리의 대퇴부 각도는 지면과 90도 이상. 값이 90 이상이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr><tr><td>right_off</td><td>dict</td><td>오른쪽 발 오프(떨어짐) 시.</td></tr><tr><td>left_off</td><td>dict</td><td>왼쪽 발 오프(떨어짐) 시.</td></tr><tr><td>opposite_knee_angle</td><td>list</td><td>오프 시 앞쪽 다리 무릎 각도 90도 이상. 값이 90 이상이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr><tr><td>opposite_elbow_angle</td><td>list</td><td>오프 시 뒤쪽 팔꿈치 각도 110도. 값이 107~113이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr><tr><td>elbow_angle</td><td>list</td><td>오프 시 앞쪽 팔꿈치 각도 90도. 값이 87~93이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr><tr><td>opposite_shoulder_angle</td><td>list</td><td>오프 시 뒤쪽 상완 지면 수직선과 80도. 값이 47~53이면 만점. 그렇지 않으면 1당 1점씩 차감.</td></tr></tbody></table>

**요청 예시**

```json
http://115.94.164.253:15003/running/get-score/example@email.com/bc692864-0243-4d41-bce3-7658c92ef0c5
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
