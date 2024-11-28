# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42861">섬 연결하기</a>

### 문제설명

n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

***

### 제한사항

 - 섬의 개수 n은 1 이상 100 이하입니다.
 - costs의 길이는 ((n-1) * n) / 2이하입니다.
 - 임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고, costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
 - 같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다. 즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
 - 모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
 - 연결할 수 없는 섬은 주어지지 않습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Edge {
    public int to;
    public int cost;
    public Edge(int _to, int _cost){
        to = _to;
        cost = _cost;
    }
}

public class Solution {
    public int solution(int n, int[,] costs) {
        int answer = 0;
        Dictionary<int, List<Edge>> graph = new Dictionary<int, List<Edge>>();
        bool[] used = new bool[n];
        int currentIndex = -1;
        int count = 0;
        List<Edge> list = new List<Edge>();
        
        for(int i = 0; i < costs.GetLength(0); i++) {
            if(!graph.ContainsKey(costs[i,0])) {
                graph[costs[i,0]] = new List<Edge>();
            }
            if(!graph.ContainsKey(costs[i,1])) {
                graph[costs[i,1]] = new List<Edge>();
            }
            graph[costs[i,0]].Add(new Edge(costs[i,1], costs[i,2]));
            graph[costs[i,1]].Add(new Edge(costs[i,0], costs[i,2]));
        }
        
        currentIndex = costs[0,0];
        used[currentIndex] = true;
        while(count != n-1) {
            list.AddRange(graph[currentIndex]);
            int min = int.MaxValue;
            int nextIndex = -1;
            for(int i = 0; i < list.Count; i++) {
                if(!used[list[i].to] && min > list[i].cost) {
                    nextIndex = list[i].to;
                    min = list[i].cost;
                }
            }
            count++;
            answer += min;
            used[nextIndex] = true;
            currentIndex = nextIndex;
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.44ms, 31.1MB)
테스트 2 〉	통과 (2.55ms, 31.3MB)
테스트 3 〉	통과 (2.45ms, 31.4MB)
테스트 4 〉	통과 (2.99ms, 31.3MB)
테스트 5 〉	통과 (2.54ms, 31.3MB)
테스트 6 〉	통과 (2.45ms, 31.4MB)
테스트 7 〉	통과 (2.44ms, 31MB)
테스트 8 〉	통과 (2.59ms, 31.4MB)
```