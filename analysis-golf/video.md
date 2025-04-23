# 골프 분석 결과 비디오 요청

## 골프 분석 결과 비디오 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-golf-video`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 골프분석 점수 값을 리턴합니다.

**파라미터(json)**

<table><thead><tr><th>Name</th><th>Type</th><th>Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td><code>id</code></td><td>string</td><td>유저 이메일 주소</td><td>true</td></tr><tr><td><code>uuid</code></td><td>string</td><td>영상 uuid</td><td>true</td></tr></tbody></table>

**응답(json)**

<table><thead><tr><th width="189">Name</th><th width="78">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>base64_video</code></td><td>string</td><td>base64로 인코딩 된 결과 비디오 문자열</td></tr></tbody></table>

**요청 예시**

```json
{
    “id”: “example@example.com”,
    “uuid”: “bc692864-0243-4d41-bce3-7658c92ef0c5”
}
```

**응답 예시**
