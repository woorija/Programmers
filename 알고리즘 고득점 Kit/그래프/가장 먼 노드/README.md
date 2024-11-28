# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49189">가장 먼 노드</a>

### 문제설명

n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 노드의 개수 n은 2 이상 20,000 이하입니다.
 - 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
 - vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int n, int[,] edge) {
        int answer = 0;
        int[] distances = new int[n];
        Dictionary<int,List<int>> graph = new Dictionary<int,List<int>>();
        List<int> nodeList = new List<int>();
        
        for(int i = 1; i < distances.Length; i++) {
            distances[i] = 20001;
        }
        for(int i = 0; i < edge.GetLength(0); i++) {
            if(!graph.ContainsKey(edge[i,0] - 1)) {
                graph.Add(edge[i,0] - 1, new List<int>());
            }
            graph[edge[i,0] - 1].Add(edge[i,1] - 1);
            if(!graph.ContainsKey(edge[i,1] - 1)) {
                graph.Add(edge[i,1] - 1, new List<int>());
            }
            graph[edge[i,1] - 1].Add(edge[i,0] - 1);
        }
        for(int i = 0; i < n; i++) {
            nodeList.Add(i);
        }
        
        while(nodeList.Count != 0){
            int current = -1;
            int currentDistance = 20001;

            for(int i = 0; i < nodeList.Count; i++) {
                if(distances[nodeList[i]] < currentDistance) {
                    current = nodeList[i];
                    currentDistance = distances[nodeList[i]];
                }
            }
            nodeList.Remove(current);
            foreach(int node in graph[current]) {
                int temp = distances[current] + 1;
                if(temp < distances[node]) {
                    distances[node] = temp;
                }
            }
        }
        
        int max = 0;
        for(int i = 0; i < distances.Length; i++) {
            if(distances[i] == max) {
                answer++;
            }else if(distances[i] > max) {
                max = distances[i];
                answer = 1;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.13ms, 31.3MB)
테스트 2 〉	통과 (3.10ms, 31.3MB)
테스트 3 〉	통과 (3.14ms, 31.3MB)
테스트 4 〉	통과 (3.23ms, 31.2MB)
테스트 5 〉	통과 (6.86ms, 31.5MB)
테스트 6 〉	통과 (7.41ms, 31.8MB)
테스트 7 〉	통과 (472.69ms, 40.5MB)
테스트 8 〉	통과 (966.78ms, 42.5MB)
테스트 9 〉	통과 (869.65ms, 42.6MB)
```