---
title: "[Algorithm]암기왕"
excerpt: "https://www.acmicpc.net/problem/2776"

categories:
  - CodingTest
tags:
  - [자료구조, 정렬 , 이분탐색, 해시를 사용한 집합과 맵]

permalink: /CodingTest/11663/

toc: true
toc_sticky: true

date: 2025-01-16
last_modified_at: 2025-01-16
---

## 🦥 본문

https://www.acmicpc.net/problem/11663
<img width="1319" alt="스크린샷 2025-01-16 오전 11 34 59" src="https://github.com/user-attachments/assets/a02b443b-5837-4587-816f-951211362a5f" />



```java
package backjoon_11663;

import java.io.*;
import java.util.Arrays;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(System.out));

        // 입력 처리
        String[] input = bufferedReader.readLine().split(" ");
        int N = Integer.parseInt(input[0]); // 점의 개수
        int M = Integer.parseInt(input[1]); // 선분의 개수
        int[] points = new int[N];

        // 점 입력
        input = bufferedReader.readLine().split(" ");
        for (int i = 0; i < N; i++) {
            points[i] = Integer.parseInt(input[i]);
        }

        // 점을 정렬
        Arrays.sort(points);

        // 선분 입력 및 처리
        for (int i = 0; i < M; i++) {
            input = bufferedReader.readLine().split(" ");
            int start = Integer.parseInt(input[0]); // 선분 시작
            int end = Integer.parseInt(input[1]);   // 선분 끝

            // 이분 탐색으로 범위 내 점 개수 계산
            int lower = lowerBound(points, start);
            int upper = upperBound(points, end);

            // 결과 출력
            bufferedWriter.write((upper - lower) + "\n");
        }

        bufferedWriter.flush();
        bufferedWriter.close();
        bufferedReader.close();
    }

    // lowerBound: 시작점 이상인 첫 번째 위치
    private static int lowerBound(int[] points, int target) {
        int left = 0, right = points.length;

        while (left < right) {
            int mid = (left + right) / 2;
            if (points[mid] >= target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }

    // upperBound: 끝점 이하인 마지막 위치 + 1
    private static int upperBound(int[] points, int target) {
        int left = 0, right = points.length;

        while (left < right) {
            int mid = (left + right) / 2;
            if (points[mid] > target) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }
}

```


<h2>개념</h2>
<h4>이분 탐색의 기본원리</h4>
<p>이분 탐색은 <Strong>정렬된 데이터</Strong>에서 원하는 값을 찾거나, 특정 조건을 만족하는 값을 찾기 위해 사용하는 알고리즘 입니다.<br/>
탐색의 범위를 절반씩 줄여나가면서 원하는 값을 효율적으로 찾아냅니다.</p>

<Strong>핵심로직</Strong><br/>

- <Strong>초기 탐색 범위</Strong>: 최소값 left와 최대값 right을 설정합니다

- <Strong>중간값 계산</Strong>:  \text{mid} = \text{left} + \frac{\text{right} - \text{left}}{2} .
- <Strong>조건 비교</Strong>: 
    1. target 이 mid보다 크다면 , 탐색 범위를 오른쪽으로 좁힘 : left = mid + 1,
    2. target이 mid 보다 작다면 , 탐색 범위를 왼쪼긍로 좁힘: right = mid - 1,
    3. target을 찾으면 종료


<h2>이분 탐색을 문제에 적응하는 요령</h2>

<Strong>1. 정렬 필요성 확인</Strong>

- 이분 탐색은 항상 <Strong>정렬된 배열</Strong>에서만 동작합니다.
- 문제에서만 입력 데이터를 정렬해야하는 경우, 반드시 정렬 후 탐색해야 함.

<Strong>2. 탐색 범위 설정</Strong>

- 문제 조건에 Left와 Right 를 설정.
- 범위 내에서 Mid를 계산하여 조건을 만족하는 지 확인.

<Strong>3. 탐색 조건 확인</Strong>

- 저간을 만족하면 reuslt 를 업데이트하거나 탐색 범위를 좁힘
- 범위를 좁히는 로직 (left = mid + 1 또는 right = mid -1)이 명확해야 함.

<Strong>4. 시간 복잡도 분석</Strong>

- 이분 탐색은 탐색 범위를 절반씩 줄이므로  O(\log N) 의 복잡도를 가짐.
- 정렬  O(N \log N) 과 결합해도 효율적.
