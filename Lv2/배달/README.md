# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12978">배달</a>

### 문제설명

N개의 마을로 이루어진 나라가 있습니다. 이 나라의 각 마을에는 1부터 N까지의 번호가 각각 하나씩 부여되어 있습니다. 각 마을은 양방향으로 통행할 수 있는 도로로 연결되어 있는데, 서로 다른 마을 간에 이동할 때는 이 도로를 지나야 합니다.

도로를 지날 때 걸리는 시간은 도로별로 다릅니다. 현재 1번 마을에 있는 음식점에서 각 마을로 음식 배달을 하려고 합니다. 각 마을로부터 음식 주문을 받으려고 하는데, N개의 마을 중에서 K 시간 이하로 배달이 가능한 마을에서만 주문을 받으려고 합니다.

마을의 개수 N, 각 마을을 연결하는 도로의 정보 road, 음식 배달이 가능한 시간 K가 매개변수로 주어질 때, 음식 주문을 받을 수 있는 마을의 개수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 마을의 개수 N은 1 이상 50 이하의 자연수입니다.
 - road의 길이(도로 정보의 개수)는 1 이상 2,000 이하입니다.
 - road의 각 원소는 마을을 연결하고 있는 각 도로의 정보를 나타냅니다.
 - road는 길이가 3인 배열이며, 순서대로 (a, b, c)를 나타냅니다.
   - a, b(1 ≤ a, b ≤ N, a != b)는 도로가 연결하는 두 마을의 번호이며, c(1 ≤ c ≤ 10,000, c는 자연수)는 도로를 지나는데 걸리는 시간입니다.
   - 두 마을 a, b를 연결하는 도로는 여러 개가 있을 수 있습니다.
   - 한 도로의 정보가 여러 번 중복해서 주어지지 않습니다.
 - K는 음식 배달이 가능한 시간을 나타내며, 1 이상 500,000 이하입니다.
 - 임의의 두 마을간에 항상 이동 가능한 경로가 존재합니다.
 - 1번 마을에 있는 음식점이 K 이하의 시간에 배달이 가능한 마을의 개수를 return 하면 됩니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Node{
    public int num;
    public int distance;
    public Node(int _num, int _distance){
        num = _num;
        distance = _distance;
    }
}
class Solution
{
    public int solution(int N, int[,] road, int K)
    {
        int answer = 0;
        int[] distances = new int[N];
        Dictionary<int,List<Node>> graph = new Dictionary<int,List<Node>>();
        List<int> nodeList = new List<int>();

        for(int i = 1; i < N; i++) {
            distances[i] = 999999;
        }
        for(int i = 0; i < road.GetLength(0); i++) {
            if(!graph.ContainsKey(road[i,0] - 1)) {
                graph.Add(road[i,0] - 1, new List<Node>());
            }
            graph[road[i,0] - 1].Add(new Node(road[i,1] - 1, road[i,2]));
            if(!graph.ContainsKey(road[i,1] - 1)) {
                graph.Add(road[i,1] - 1, new List<Node>());
            }
            graph[road[i,1] - 1].Add(new Node(road[i,0] - 1, road[i,2]));
        }
        for(int i = 0; i < N; i++) {
            nodeList.Add(i);
        }
        
        while(nodeList.Count != 0) {
            int current = -1;
            int currentDistance = 999999;
            for(int i = 0; i < nodeList.Count; i++) {
                if(distances[nodeList[i]] < currentDistance) {
                    current = nodeList[i];
                    currentDistance = distances[nodeList[i]];
                }
            }
            nodeList.Remove(current);
            foreach(Node node in graph[current]) {
                int temp = distances[current] + node.distance;
                if(temp < distances[node.num]) {
                    distances[node.num] = temp;
                }
            }
        }
        
        
        for(int i = 0; i < distances.Length; i++) {
            if(distances[i] <= K) {
                answer++;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.39ms, 31.3MB)
테스트 2 〉	통과 (3.31ms, 31.1MB)
테스트 3 〉	통과 (3.32ms, 31.2MB)
테스트 4 〉	통과 (3.21ms, 31.2MB)
테스트 5 〉	통과 (3.33ms, 31.3MB)
테스트 6 〉	통과 (3.30ms, 31.3MB)
테스트 7 〉	통과 (3.36ms, 31.2MB)
테스트 8 〉	통과 (3.35ms, 31.2MB)
테스트 9 〉	통과 (3.16ms, 31.2MB)
테스트 10 〉	통과 (3.41ms, 31.4MB)
테스트 11 〉	통과 (3.35ms, 31.3MB)
테스트 12 〉	통과 (3.41ms, 31.2MB)
테스트 13 〉	통과 (5.10ms, 31.4MB)
테스트 14 〉	통과 (3.51ms, 31.5MB)
테스트 15 〉	통과 (3.64ms, 31.5MB)
테스트 16 〉	통과 (3.38ms, 31.4MB)
테스트 17 〉	통과 (3.61ms, 31.5MB)
테스트 18 〉	통과 (3.56ms, 31.3MB)
테스트 19 〉	통과 (3.60ms, 31.7MB)
테스트 20 〉	통과 (3.44ms, 31.5MB)
테스트 21 〉	통과 (3.75ms, 31.6MB)
테스트 22 〉	통과 (3.46ms, 30.9MB)
테스트 23 〉	통과 (3.69ms, 31.4MB)
테스트 24 〉	통과 (3.73ms, 31.5MB)
테스트 25 〉	통과 (3.79ms, 31.8MB)
테스트 26 〉	통과 (3.78ms, 31.7MB)
테스트 27 〉	통과 (3.76ms, 31.6MB)
테스트 28 〉	통과 (3.83ms, 31.8MB)
테스트 29 〉	통과 (4.80ms, 31.6MB)
테스트 30 〉	통과 (4.13ms, 31.5MB)
테스트 31 〉	통과 (3.40ms, 30.9MB)
테스트 32 〉	통과 (3.38ms, 30.9MB)
```