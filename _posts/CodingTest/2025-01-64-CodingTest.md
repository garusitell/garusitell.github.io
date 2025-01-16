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

date: 2025-01-14
last_modified_at: 2025-01-14
---

## 🦥 본문

https://www.acmicpc.net/problem/11663

<img width="1319" alt="image" src="https://github.com/user-attachments/assets/f48c4be8-ced2-4b07-bffd-d118403dc7c3" />


```java
package backjoon_2776;

import java.io.*;
import java.util.Arrays;

public class Study_main {
    public static void main(String[] args) throws NumberFormatException, IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new OutputStreamWriter(System.out));

        int testCase = Integer.parseInt(bufferedReader.readLine());
        for(int i = 0 ; i <testCase ; i++)
        {
            int N = Integer.parseInt(bufferedReader.readLine());
            String[] input = bufferedReader.readLine().split(" ");//공백을 기준으로 나눈다

            int[] note = new int[N];
            for(int j = 0; j < N; j++){
                note[j] = Integer.parseInt(input[j]);
            }

            Arrays.sort(note);

            int M = Integer.parseInt(bufferedReader.readLine());
            input = bufferedReader.readLine().split(" ");
            for(int j = 0; j < M; j++){
                int findNumber = Integer.parseInt(input[j]);

                int start = 0;
                int end  = N - 1;
                boolean find = false;
                while(start <= end){
                    int mid = (start + end) / 2;

                    if(note[mid] == findNumber){
                        bufferedWriter.write(1+"\n");
                        find = true;
                        break;
                    }else if(note[mid] > findNumber){
                        end = mid-1;
                    }else{
                        start = mid + 1;
                    }
                }
                if(!find){
                    bufferedWriter.write(0+"\n");
                }
            }
            bufferedWriter.flush();
            bufferedWriter.close();
            bufferedReader.close();

        }
    }
}

```
