# 골프 분석 결과 비디오 요청

## 골프 분석 결과 비디오 요청

<mark style="color:green;">`POST`</mark> `http://api.remo.re.kr/api/analysis-golf-draw`

사용자 id(이메일), 분석된 비디오 uuid를 파라미터로 받아 골프분석 결과 비디오를 리턴합니다.

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

{% tabs %}
{% tab title="200" %}
```
{
    "base64_video": "AAAAIGZ0eXBpc29tAAACAGlzb21pc28yYXZjMW1wNDEAAAAIZnJlZQAK/7BtZGF0AAACugYF … (이하 생략)"
}
```
{% endtab %}
{% endtabs %}

**에러 코드 안내**

| 대분류          | 소분류                      | 코드  |
| ------------ | ------------------------ | --- |
| 입력 데이터 문제 발생 | 필수 데이터 없음                | 413 |
| 분석 이슈        | 트래킹 된 사람이 없음             | 511 |
|              | 트래킹 구간이 너무 짧음(최소 30 프레임) | 512 |
|              | 골프 결과 분석 이슈              | 520 |
|              | 결과 파일 없음                 | 533 |
|              | 분석 중 또는 로그 파일 생성되지 않음    | 534 |
