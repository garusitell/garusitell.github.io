---
title: "[Algorithm]DFS와 BFS"
excerpt: "https://www.acmicpc.net/problem/1260"

categories:
  - CodingTest
tags:
  - [자료구조,BFS,DFS,STACK,QUEUE,LINKEDLIST]

permalink: /CodingTest/1260/

toc: true
toc_sticky: true

date: 2025-01-20
last_modified_at: 2025-01-20
---

## 🦥 본문

https://www.acmicpc.net/problem/1260
![Image](https://github.com/user-attachments/assets/01b91bf8-6048-4c66-b942-58313dbcaa94)

<h2>스택으로로 푼 DFS</h2>
<br>

```java
package backjoon_1260;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.*;

public class Main_withStack {
    static StringBuilder sb = new StringBuilder();
    static boolean[] check; // 방문 체크
    static ArrayList<Integer>[] adjList; // 인접 리스트
    static int node, line, start; // 노드 수, 간선 수, 시작 노드

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        node = Integer.parseInt(st.nextToken());
        line = Integer.parseInt(st.nextToken());
        start = Integer.parseInt(st.nextToken());

        // 인접 리스트 초기화
        adjList = new ArrayList[node + 1];
        for (int i = 1; i <= node; i++) {
            adjList[i] = new ArrayList<>();
        }

        // 그래프 입력
        for (int i = 0; i < line; i++) {
            st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            adjList[a].add(b);
            adjList[b].add(a);
        }

        // 방문 순서를 위해 정렬
        for (int i = 1; i <= node; i++) {
            Collections.sort(adjList[i]);
        }

        // DFS (스택 이용)
        check = new boolean[node + 1];
        dfsWithStack(start);

        // BFS
        sb.append("\n");
        check = new boolean[node + 1];
        bfs(start);

        // 결과 출력
        System.out.println(sb);
    }

    // 스택을 이용한 DFS
    private static void dfsWithStack(int start) {
        Stack<Integer> stack = new Stack<>();
        stack.push(start); // 시작 노드 삽입

        while (!stack.isEmpty()) {
            int cur = stack.pop(); // 스택에서 노드 꺼냄

            if (!check[cur]) { // 방문하지 않은 경우 처리
                check[cur] = true;
                sb.append(cur).append(" ");

                // 인접 노드를 스택에 추가 (역순으로 추가해 작은 번호 우선 탐색)
                for (int i = adjList[cur].size() - 1; i >= 0; i--) {
                    int next = adjList[cur].get(i);
                    if (!check[next]) {
                        stack.push(next);
                    }
                }
            }
        }
    }

    // 큐를 이용한 BFS
    private static void bfs(int start) {
        Queue<Integer> queue = new LinkedList<>();
        queue.add(start);
        check[start] = true;

        while (!queue.isEmpty()) {
            int cur = queue.poll();
            sb.append(cur).append(" ");

            for (int next : adjList[cur]) {
                if (!check[next]) {
                    queue.add(next);
                    check[next] = true;
                }
            }
        }
    }
}
```

<h2>재귀로 푼 DFS</h2>
<br/>

```java

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {
    static StringBuilder sb = new StringBuilder();
    static boolean[] check;
    static int[][] arr;

    static int node,line,start;

    static Queue<Integer> q= new LinkedList<>();
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        node = Integer.parseInt(st.nextToken());
        line = Integer.parseInt(st.nextToken());
        start = Integer.parseInt(st.nextToken());

        arr = new int[node+1][node+1];
        check = new boolean[node+1];

        for(int i = 0 ; i < line ; i++ ){
            StringTokenizer str = new StringTokenizer(br.readLine());

            int a = Integer.parseInt(str.nextToken());
            int b = Integer.parseInt(str.nextToken());

            arr[a][b] = arr[b][a] = 1;

        }
        dfs(start);
        sb.append("\n");
        check = new boolean[node+1];

        bfs(start);

        System.out.println(sb);



    }



    private static void dfs(int start) {
        check[start] = true;
        sb.append(start + " ");
        for(int i = 1 ; i <= node ; i++){
            if(arr[start][i] == 1 && check[i] == false){
                dfs(i);
            }
        }

    }


    private static void bfs(int start) {
        q.add(start);
        check[start] = true;

        while(!q.isEmpty()){
            start= q.poll();
            sb.append(start + " ");

            for(int i = 1 ; i <= node ; i++){
                if(arr[start][i] == 1 && check[i] == false){
                    q.add(i);
                    check[i] = true;
                }
            }

        }
    }
}

```

<h2>너비 우선 탐색(BFS,Breadth-First Search)</h2>
<br/>

- 시작 정점 방문 후 가까운 정점 우선 방문
- 넓게 탐색하는 방법
- 두 노드 사이 최단거리 , 최단 경로 구할 때 자주 사용
- 장점
    - 최적해 찾음 보장
- 단점
    - 최소 실행보다 오래 걸립니다.

<h4>기본 구현</h4>
<hr/>
1. 정점 v에 방문한다.<br/>
2.정점 v에 인점한 정점 중 방문하지 않은 정점을 차례로 방문하면서 큐에 넣는다.<br/>
3.인접합 정점 모두 방분했다면 큐에서 dequeue하여 받은 값 정점 v로 설정하고 2를 반복한다.<br/>
4.큐가 공백이라면 탐색 완료한 것이다.
<br/><br/><br/>



```Java
static boolean[] visit;
static LinkedList<Integer>[] graph;
static int[][] graph;

//시작 정점 v
Public static void bfs(int v){
    Queue<Integer> queue = new LinkedList<>();
    queue.add(v);
    visit[v] = true;

    while(!queue.isEmpty()){
        int temp = queue.poll();
        System.out.println(temp);

        for(int nextV: graph[temp]){
            if(!visit[nextV]){
                queue.add(nextV);
                visit[nextV] = true;
            }
        }
    }
}
```
<hr/><br/>
<h2>깊이 우선 탐색(DFS,Dreadth-First Search)</h2>
<br/>

- 시작 정점 방문 후 다음 분기로 넘어가기 전 해당 분기 완벽하게 탐색
- 트리에서 보면 노드 방문 후 자식 노드 우선 방문
- 깊이 탐색하는 방법
- 장점
    - 최선의 경우 빠르게 해를 찾음
- 단점
    - 찾은 해가 최적 해가 아닐 가능성 있음
    - 최악의 경우 해 찾는데 가장 오랜 시간 걸림



<h4>기본 구현</h4>
<br/>
1.정점 v를 방분한다.<br/>
2.정점 v에서 인접한 정점 중에 방문하지 않은 정점 w가 있다면 w를 v로 하여 1부터 반복한다(재귀함수 호출)<br/>
3.인접한 정점 모두 방문했다면 스택에서 정점을 꺼내 위를 반복한다.<br/>
<br/><br/><br/>

```java
//시작 정점 v
static boolean[] visit;
//연결 리스트, 행렬 그래프 중 선택
static LinkedList<Integer>[] graph;
static int[][]graph;

public static void dfs(int v){
    visit[v] = true;
    System.out.println(v);
    for(int nextV: graph[v]){
        if(!visit[nextV]defs (nextV));
    }
}
```

<h2>시간 복잡도</h2>
<br/>

- BFS DFS 둘의 시간 복잡도는 동일하며 , 그래프 구현에 따라 시간 복잡도가 달라짐
- 연결 리스트로 구현한 그래프:O(n+m)
- 행렬로 구현한 그래프 : O(n^2)