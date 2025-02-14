# BOJ 16637번 [괄호 추가하기](https://www.acmicpc.net/problem/16637)

## 🌈 풀이 후기
문제를 2번읽자!  
괄호 안에 연산자가 1개만 들어있어야 한다는 조건을 늦게봐서 중간에 다 지우고 다시 풀었습니다. 😢

</br></br>

## 👩‍🏫 문제 풀이

### 변수

* max  
출력조건 `정답은 2^31 보다 작고, -2^31 보다 크다.` 에 따라 int형의 최솟값으로 초기화했습니다.

### 풀이 방법
* 예시  
1-2+3*4

#### 괄호 계산

1. 괄호가 있을 때는 index+2 부터 index+4 까지 괄호의 범위라고 생각합니다.  
초기 result 에는 수식의 첫번째 숫자를 넣습니다.


||1|-|2|+|3|*|4|
|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|
|현재 index|v|||||||
|괄호|||(||)|||
* result=1;
* tempResult=calc(2, +, 3); -> tempResult=5
* tempResult=calc(result, -, tempResult); -> tempResult= 1-5=-4
* recursion(index+4, tempResult);
2. 
||1|-|2|+|3|*|4|
|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|
|현재 index|||||v|||
* result= -4
* index+4 가 N의 범위를 벗어나므로 괄호를 넣을 수 없습니다.

#### 괄호 없는 계산
3. 괄호가 없는 계산은 index부터 index+2 까지 계산합니다.

||1|-|2|+|3|*|4|
|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|
|현재 index|||||v|||
* result= -4
* tempResult=calc(-4, *, 4); ->tempResult=-16
* recutsion(index+2, tempResult);

4. 
||1|-|2|+|3|*|4|
|---|---|---|---|---|---|---|---|
|index|0|1|2|3|4|5|6|
|현재 index|||||||v|
* result= -16
* index==N-1 이므로 수식이 끝났습니다. 
* max 값과 result 값을 비교한 후, 더 큰 값을 max값에 넣습니다.