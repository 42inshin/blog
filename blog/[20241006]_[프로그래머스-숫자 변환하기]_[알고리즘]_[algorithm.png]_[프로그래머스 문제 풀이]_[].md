# [level 2] 숫자 변환하기 - 154538

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

> 출처: 프로그래머스 코딩 테스트 연습 [(문제 링크)](https://school.programmers.co.kr/learn/courses/30/lessons/154538?language=javascript)

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

  return arr[y];
}
```

> DFS로 풀었을 때 시간초과가 발생하여 DP로 풀었습니다. DFS로 풀었을 때는 모든 경우의 수를 탐색하기 때문에 시간복잡도가 O(3^y)가 되어 시간초과가 발생합니다. DP로 풀었을 때는 중복되는 연산을 줄여 시간복잡도를 O(y)로 줄일 수 있습니다.


### 풀이 설명

`x = 2, y = 10, n = 3`인 경우를 예시로 들어 단계별 분석을 해보겠습니다.

초기화 배열을 만들어 x부터 y 인덱스까지의 값을 -1로 초기화합니다. x의 값을 0으로 초기화합니다. x부터 y까지 반복문을 돌면서 다음과 같은 연산을 수행합니다.

**초기화 배열**
```js
arr = [-1, -1, 0, -1, -1, -1, -1, -1, -1, -1, -1]
```

**수행할 연산**
1. `x + n`
2. `x * 2`
3. `x * 3`

연산을 수행할 때 `y`보다 작거나 같은 경우에만 연산을 수행합니다. 연산을 수행할 때 `arr[i]`가 `-1`이면 연산을 수행하지 않습니다. 해당 인덱스와 동일한 값에 도달할 수 없기 때문입니다. 연산을 수행할 때 `arr[i + n]`이 `-1`이면 `arr[i + n]`에 `arr[i] + 1`을 할당합니다. `arr[i + n]`이 `-1`이 아니면 `arr[i] + 1`과 `arr[i + n]` 중 작은 값을 할당합니다. 이를 반복하면 `y`까지의 최소 연산 횟수를 구할 수 있습니다.


#### 첫 번째 반복 (i = 2) 인 경우, x + n, x * 2, x * 3 연산을 수행합니다.

```js
arr = [-1, -1, 0, -1, 1, 1, 1, -1, -1, -1, -1]
```

#### 두 번째 반복 (i = 3) 인 경우, -1이기 때문에, 숫자 3은 도달할 수 없습니다. 따라서 건너뜁니다.

#### 세 번째 반복 (i = 4) 인 경우, 1이므로 x + n, x * 2, x * 3 연산을 수행합니다.

```js
arr = [-1, -1, 0, -1, 1, 1, 1, 2, 2, -1, -1]
```

#### 네 번째 반복 (i = 5) 인 경우, `arr[5] = 1`이므로, 여기서 다음 숫자들로 이동합니다.

- `5 + 3 = 8`: `arr[8] = 2`이지만, `arr[5] + 1 = 2`로 같으므로 변경하지 않습니다.
- `5 * 2 = 10`: `arr[10]`이 `-1`이므로 `arr[10]`을 `arr[5] + 1 = 2`로 설정합니다.
- `5 * 3 = 15`: `15`는 `y = 10`보다 크므로 무시합니다.

```js
arr = [-1, -1, 0, -1, 1, 1, 1, 2, 2, -1, 2]
```

#### 이후 반복
`arr[6], arr[7], arr[8], arr[9]` 모두 이런 방식대로 반복하면 값을 구할 수 있습니다.<br/>
사실 `arr[10] = 2`로 최소 단계를 기록했으므로, 더 이상 탐색할 필요가 없습니다.

#### 최종 결과
최종적으로 `arr[y] = arr[10] = 2`이므로, `x = 2`에서 `y = 10`으로 가는 최소 단계는 `2`입니다.<br/>
즉, `2 → 5 → 10`의 경로로 최소 2단계 만에 도달할 수 있습니다.

```js
arr = [-1, -1, 0, -1, 1, 1, 1, 2, 2, 2, 2]
```
