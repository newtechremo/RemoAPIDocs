---
description: 완료된 달리기 분석 결과를 요청하는 API입니다.
---

# 달리기 분석 결과 요청

## 달리기 분석 결과 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-running-result`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 달리기분석 결과 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="126">Name</th><th width="86">Type</th><th>Description</th></tr></thead><tbody><tr><td>right_contact</td><td>dict</td><td>오른쪽 발 컨택 시.</td></tr><tr><td>left_contact</td><td>dict</td><td>왼쪽 발 컨택 시.</td></tr><tr><td>ankle_location</td><td>list</td><td>컨택 시 발 위치는 몸 중심보다 뒤로 가있어야 함. 해당 값은 발목 위치에서 몸 중심 위치를 뺀 값. Left/RightAnkleCoordX - CenterCoordX 참고.</td></tr><tr><td>ankle_angle</td><td>list</td><td>컨택 시 발목 각도가 0도에 가까워야 함. Left/RightAnkle(z) 참고.</td></tr><tr><td>opposite_thigh_angle</td><td>list</td><td>컨택 시 반대쪽 다리의 대퇴부 각도는 지면과 90도 이상. GLeft/RightHip(z) 참고.</td></tr><tr><td>right_off</td><td>dict</td><td>오른쪽 발 오프(떨어짐) 시</td></tr><tr><td>left_off</td><td>dict</td><td>왼쪽 발 오프(떨어짐) 시</td></tr><tr><td>opposite_knee_angle</td><td>list</td><td>오프 시 앞쪽 다리 무릎 각도 90도 이상. Left/RightKnee(x) 참고.</td></tr><tr><td>opposite_elbow_angle</td><td>list</td><td>오프 시 뒤쪽 팔꿈치 각도 110도. Left/RightElbow(x) 참고.</td></tr><tr><td>elbow_angle</td><td>list</td><td>오프 시 앞쪽 팔꿈치 각도 90도. Left/RightElbow(x) 참고.</td></tr><tr><td>opposite_shoulder_angle</td><td>list</td><td>오프 시 뒤쪽 상완 지면 수직선과 80도. Left/RightShoulder(x) 참고.</td></tr></tbody></table>

**요청 예시**

```json
/analysis-running-result/example@email.com/bc692864-0243-4d41-bce3-7658c92ef0c5
```

**응답 예시**

{% tabs %}
{% tab title="200" %}
```json
{
  "right_contact": {
    "ankle_location": [
      86.815,
      22.370000000000005,
      7.109999999999985
    ],
    "ankle_angle": [
      4.093964842889073,
      5.774488215914294,
      -2.446931225250296
    ],
    "opposite_thigh_angle": [
      -98.48843215577908,
      -102.10886516814739,
      -98.59040979513446
    ]
  },
  "left_contact": {
    "ankle_location": [
      135.42999999999998,
      -32.254999999999995
    ],
    "ankle_angle": [
      6.248219067433043,
      4.790707770474713
    ],
    "opposite_thigh_angle": [
      -88.87852463333832,
      -101.85463117532001
    ]
  },
  "right_off": {
    "opposite_knee_angle": [
      123.80539368950052,
      122.07162243024348,
      130.2339776437497
    ],
    "opposite_elbow_angle": [
      97.4101326409947,
      101.6721883619544,
      108.00697951183741
    ],
    "elbow_angle": [
      79.91231235665491,
      81.69285425350515,
      90.36005259415758
    ],
    "opposite_shoulder_angle": [
      -38.27896818679298,
      -35.42633139498491,
      -28.369690805409753
    ]
  },
  "left_off": {
    "opposite_knee_angle": [
      86.76502387152419,
      105.79557009345625
    ],
    "opposite_elbow_angle": [
      110.78887599666596,
      106.77383145038354
    ],
    "elbow_angle": [
      52.75517901107695,
      51.738353214487745
    ],
    "opposite_shoulder_angle": [
      -37.47948255416166,
      -50.58117271101567
    ]
  }
}

```
{% endtab %}
{% endtabs %}
