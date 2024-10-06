# [level 2] 숫자 변환하기 - 154538

[문제 링크](https://school.programmers.co.kr/learn/courses/30/lessons/154538?language=javascript)

### 성능 요약

메모리: 41.3 MB, 시간: 40.28 ms

### 구분

코딩테스트 연습 > 연습문제

### 채점결과

정확성: 100.0<br/>합계: 100.0 / 100.0

### 제출 일자

2024년 10월 06일 15:14:32

### 문제 설명

<p>자연수 <code>x</code>를 <code>y</code>로 변환하려고 합니다. 사용할 수 있는 연산은 다음과 같습니다.</p>

<ul>
<li><code>x</code>에 <code>n</code>을 더합니다</li>
<li><code>x</code>에 2를 곱합니다.</li>
<li><code>x</code>에 3을 곱합니다.</li>
</ul>

<p>자연수 <code>x</code>, <code>y</code>, <code>n</code>이 매개변수로 주어질 때, <code>x</code>를 <code>y</code>로 변환하기 위해 필요한 최소 연산 횟수를 return하도록 solution 함수를 완성해주세요. 이때 <code>x</code>를 <code>y</code>로 만들 수 없다면 -1을 return 해주세요.</p>

<hr>

<h5>제한사항</h5>

<ul>
<li>1&nbsp;≤&nbsp;<code>x</code> ≤ <code>y</code>&nbsp;≤ 1,000,000</li>
<li>1 ≤ <code>n</code> &lt; <code>y</code></li>
</ul>

<hr>

<h5>입출력 예</h5>
<table class="table">
        <thead><tr>
<th>x</th>
<th>y</th>
<th>n</th>
<th>result</th>
</tr>
</thead>
        <tbody><tr>
<td>10</td>
<td>40</td>
<td>5</td>
<td>2</td>
</tr>
<tr>
<td>10</td>
<td>40</td>
<td>30</td>
<td>1</td>
</tr>
<tr>
<td>2</td>
<td>5</td>
<td>4</td>
<td>-1</td>
</tr>
</tbody>
      </table>
<hr>

<h5>입출력 예 설명</h5>

<p>입출력 예 #1<br>
<code>x</code>에 2를 2번 곱하면 40이 되고 이때가 최소 횟수입니다.</p>

<p>입출력 예 #2<br>
<code>x</code>에 <code>n</code>인 30을 1번 더하면 40이 되고 이때가 최소 횟수입니다.</p>

<p>입출력 예 #3<br>
<code>x</code>를 <code>y</code>로 변환할 수 없기 때문에 -1을 return합니다.</p>

> 출처: 프로그래머스 코딩 테스트 연습, https://school.programmers.co.kr/learn/challenges

### 풀이

```javascript
function solution(x, y, n) {
  let arr = new Array(y + 1).fill(-1);
  arr[x] = 0;

  for (let i = x; i <= y; i++) {
    if (arr[i] == -1) continue;
    // x + n
    if (i + n <= y) {
      if (arr[i + n] == -1) arr[i + n] = arr[i] + 1;
      else arr[i + n] = Math.min(arr[i] + 1, arr[i + n]);
    }

    // x * 2
    if (i * 2 <= y) {
      if (arr[i * 2] == -1) arr[i * 2] = arr[i] + 1;
      else arr[i * 2] = Math.min(arr[i] + 1, arr[i * 2]);
    }
    // x * 3
    if (i * 3 <= y) {
      if (arr[i * 3] == -1) arr[i * 3] = arr[i] + 1;
      else arr[i * 3] = Math.min(arr[i] + 1, arr[i * 3]);
    }
  }
  console.log(arr);
  return arr[y];
}
```

### 설명

DFS로 풀었을 때 시간초과가 발생하여 DP로 풀었습니다. DFS로 풀었을 때는 모든 경우의 수를 탐색하기 때문에 시간복잡도가 O(3^y)가 되어 시간초과가 발생합니다. DP로 풀었을 때는 중복되는 연산을 줄여 시간복잡도를 O(y)로 줄일 수 있습니다.
