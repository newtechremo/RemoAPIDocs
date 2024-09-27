---
description: 완료된 골프 분석 결과를 요청하는 API입니다.
---

# 골프 분석 결과 요청

## 골프 분석 결과 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-golf-result`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 골프분석 결과 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="185">Category</th><th width="126">Name</th><th width="86">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>address</code></td><td><code>stance</code></td><td>float</td><td>스탠스 폭. AnkleShoulderRatio 참고.</td></tr><tr><td></td><td><code>upper_body_tilt</code></td><td>float</td><td> 상체 기울임 정도. HipNeckRatio 참고.</td></tr><tr><td></td><td><code>shoulder_tilt</code></td><td>float</td><td>어깨 기울임 정도. UpperBody(z) 참고.</td></tr><tr><td></td><td><code>head_location</code></td><td>float</td><td>기준 머리 위치. 점수에는 반영하지 않음.</td></tr><tr><td><code>takeback</code></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. LeftElbow(x) 참고.</td></tr><tr><td></td><td><code>right_arm_flexion</code></td><td>float</td><td>오른팔 펴짐 각도. RightElbow(x) 참고.</td></tr><tr><td><code>backswing</code></td><td><code>head_location</code></td><td>float</td><td>머리 위치. { HeadLocation(backswing) - HeadLocation(address) } / height 참고.</td></tr><tr><td></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. LeftElbow(x) 참고.</td></tr><tr><td><code>backswingtop</code></td><td><code>reverse_spine</code></td><td>float</td><td>리버스 스파인. -Spine2(x) 참고.</td></tr><tr><td></td><td><code>right_leg_flexion</code></td><td>float</td><td>오른 다리 펴짐 각도. RightKnee(x) 참고.</td></tr><tr><td></td><td><code>head_location</code></td><td>float</td><td>머리 위치. { HeadLocation(top) - HeadLocation(address) } / height 참고.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. AnkleHipRatio 참고.</td></tr><tr><td><code>downswing</code></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. AnkleHipRatio 참고.</td></tr><tr><td></td><td><code>right_elbow_location</code></td><td>float</td><td>오른팔꿈치 위치. LeftElbowCoordY - RightElbowCoordY > 0 참고.</td></tr><tr><td></td><td><code>right_arm_rotation</code></td><td>float</td><td>오른팔-겨드랑이 각도. RightShoulder(y) 참고.</td></tr><tr><td><code>impact</code></td><td><code>head_location</code></td><td>float</td><td>머리 위치. { HeadLocation(impact) - HeadLocation(address) } / height 참고.</td></tr><tr><td></td><td><code>left_arm_flexion</code></td><td>float</td><td>왼팔 펴짐 각도. LeftElbow(x) 참고.</td></tr><tr><td></td><td><code>right_arm_flexion</code></td><td>float</td><td>오른팔 펴짐 각도. RightElbow(x) 참고.</td></tr><tr><td><code>follow</code></td><td><code>left_line_align</code></td><td>float</td><td>왼쪽 라인 일직선 정도. LAnkleLHipHori 참고.</td></tr><tr><td></td><td><code>chicken_wing</code></td><td>float</td><td>치킨윙(왼팔 펴짐 각도). LeftElbow(x) 참고.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. AnkleHipRatio 참고.</td></tr><tr><td><code>finish</code></td><td><code>left_foot_fix</code></td><td>float</td><td>왼발 고정 여부. GLeftAnkle(y) 참고.</td></tr><tr><td></td><td><code>right_foot_rotation</code></td><td>float</td><td>오른발 회전 여부. GRightHip(y) 참고.</td></tr><tr><td></td><td><code>center_of_gravity</code></td><td>float</td><td>무게 중심. LAnkleRHipHori 참고.</td></tr></tbody></table>

**요청 예시**

```json
/analysis-golf-result/example@email.com/bc692864-0243-4d41-bce3-7658c92ef0c5
```

**응답 예시**

{% tabs %}
{% tab title="200" %}
```json
{
  "address": {
    "stance": 1.5488772877619008,
    "upper_body_tilt": 0.4854274709141993,
    "shoulder_tilt": -0.2616089987804697,
    "head_location": 1334.8835885631015
  },
  "takeback": {
    "left_arm_flexion": -4.980126311547378,
    "right_arm_flexion": -24.714458935928302
  },
  "backswing": {
    "head_location": 0.28434030464154886,
    "left_arm_flexion": -27.18974815417651
  },
  "backswingtop": {
    "reverse_spine": -16.628534907215645,
    "right_leg_flexion": 31.095540126823145,
    "head_location": 0.2693764822362198,
    "center_of_gravity": 0.5588707005491961
  },
  "downswing": {
    "center_of_gravity": 0.3786936849238848,
    "right_elbow_location": 65.3828829419507,
    "right_arm_rotation": 0.9106984670157443
  },
  "impact": {
    "head_location": -0.15577396189399054,
    "left_arm_flexion": -22.75064619355969,
    "right_arm_flexion": -23.467909887523447
  },
  "follow": {
    "left_line_align": 9.159149731780538,
    "chicken_wing": -23.49651895953,
    "center_of_gravity": 0.717617472119026
  },
  "finish": {
    "left_foot_fix": 8.19698657916239,
    "right_foot_rotation": 19.20673535624702,
    "center_of_gravity": 4.18974060680288
  }
}

```
{% endtab %}
{% endtabs %}
