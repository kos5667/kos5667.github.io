---
layout: post
title: "[백준]10986 나머지 합 풀이"
excerpt_image: "../assets/images/excerpt-2024-09-24-Algorithm-Backjoon-G310986.png"
categories: Algorithm
tags: [Algorithm, Java]
allow_publishing: true
---
### 문제
**[10986 나머지 합](https://www.acmicpc.net/problem/10986)**

### 풀이
#### 1. 변수 선언 
1. N은 10⁶(1,000,000), M은 10³(1,000), N개의 수 10⁹(1,000,000,000)

2. N개의 수는 최악에 경우 1,000,000,000을 넘길 수 있습니다.

   > [!WARNING]
   >
   > int[] 최대 범위 ~ 2,147,483,647, N개의 수는 범위를 넘지 않기 때문에 int[]을 선언하여 알고리즘을 풀이 하지만 ArrayIndexOutOfBoundsException가 발생하여 long[] 전환하여 문제를 해결하였습니다.
   >
   > [**!!ArrayIndexOutOfBoundsException**](https://help.acmicpc.net/judge/rte/IndexOutOfBounds)

3. N개의 수는 new long[N] 으로 받습니다.

#### 2. 합 배열 생성
'**연속된 부분 구간의 합**'은 합 배열을 통해 쉽게 구할 수 있습니다.
구간의 누적 합을 미리 계산하여 배열로 만들어 둡니다.

#### 3. 누적 합을 M으로 나눈 나머지 값을 담은 배열 생성
‘**M으로 나누어 떨어지는** 구간의 개수’ 누적 합 배열을 이용하여 M으로 나눈 나머지 값을 구합니다

#### 4. 나머지 값을 담은 배열의 i, j 쌍의 개수를 이루는 경우의 수 구하기
3번에서 구한 배열의 수를 M으로 나눈 나머지 값을 이용하여 ‘**M으로 나누어 떨어지는 (i, j) 쌍의 개수**’를 구합니다.


### 예제
#### 1. 주어진 수열 [1, 2, 3, 1, 2, 3], M = 3
1. 합배열 = [1, 3, 6, 7, 9, 12]
2. M으로 나눈 나머지 값 = [1, 0, 0, 1, 0, 0]
3. 경우의 수
   - 나머지 값 0의 개수: 4
   - 0의 개수: 4 ｘ (4 - 1) ÷ 2 = 6
   - 1의 개수: 2 ｘ (2 - 1) ÷ 2 = 1
4. 총 경우의 수: 4 + 6 + 1

**총 개수** = 11

#### 2. 주어진 수열 [1, 2, 6, 5, 7, 12, 4], M = 5
1. 합배열 = [1, 3, 9, 14, 21, 33, 37]
2. M으로 나눈 나머지 값 = [1, 3, 4, 4, 1, 3, 2]
3. 경우의 수
   - 나머지 값 0의 개수: 0
   - 1의 개수: 2 ｘ (2 - 1) ÷ 2 = 1
   - 2의 개수: 1 ｘ (1 - 1) ÷ 2 = 0
   - 3의 개수: 2 ｘ (2 - 1) ÷ 2 = 1
   - 4의 개수: 2 ｘ (2 - 1) ÷ 2 = 1
4. 총 경우의 수: 0 + 1 + 0 + 1 + 1

**총 개수** = 3

#### 3. 주어진 수열 [3, 2, 4, 8, 7, 12, 13, 9], M = 2
1. 합배열 = [3, 5, 9, 17, 24, 36, 49, 58]
2. M으로 나눈 나머지 값 = [1, 1, 1, 1, 0, 0, 1, 0]
3. 경우의 수
   - 나머지 값 0의 개수: 3
   - 0의 개수: 3 ｘ (3 - 1) ÷ 2 = 3
   - 1의 개수: 5 ｘ (5 - 1) ÷ 2 = 10
4. 총 경우의 수: 3 + 3 + 10

**총 개수** = 16

### 코드

```java
public static void main(String[] args) throws IOException {
    Scanner sc = new Scanner(System.in);
    int n = sc.nextInt();
    int m = sc.nextInt();

    long[] s = new long[n];
    for (int i=0; i<n; i++) {
        s[i] = i == 0 ? sc.nextInt() : s[i-1] + sc.nextInt();
    }

    int[] c = new int[m];
    for (long i : s) {
        c[(int) (i % m)]++;
    }

    long answer = c[0];
    for (int i=0; i<m; i++) {
        answer += c[i] * (c[i] - 1) / 2;
    }
    
    System.out.println(answer);
}
```

