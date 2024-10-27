# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/132266">부대복귀</a>

### 문제설명

강철부대의 각 부대원이 여러 지역에 뿔뿔이 흩어져 특수 임무를 수행 중입니다. 지도에서 강철부대가 위치한 지역을 포함한 각 지역은 유일한 번호로 구분되며, 두 지역 간의 길을 통과하는 데 걸리는 시간은 모두 1로 동일합니다. 임무를 수행한 각 부대원은 지도 정보를 이용하여 최단시간에 부대로 복귀하고자 합니다. 다만 적군의 방해로 인해, 임무의 시작 때와 다르게 되돌아오는 경로가 없어져 복귀가 불가능한 부대원도 있을 수 있습니다.

강철부대가 위치한 지역을 포함한 총지역의 수 n, 두 지역을 왕복할 수 있는 길 정보를 담은 2차원 정수 배열 roads, 각 부대원이 위치한 서로 다른 지역들을 나타내는 정수 배열 sources, 강철부대의 지역 destination이 주어졌을 때, 주어진 sources의 원소 순서대로 강철부대로 복귀할 수 있는 최단시간을 담은 배열을 return하는 solution 함수를 완성해주세요. 복귀가 불가능한 경우 해당 부대원의 최단시간은 -1입니다.

***

### 제한사항

 - 3 ≤ n ≤ 100,000
   - 각 지역은 정수 1부터 n까지의 번호로 구분됩니다.
 - 2 ≤ roads의 길이 ≤ 500,000
   - roads의 원소의 길이 = 2
   - roads의 원소는 [a, b] 형태로 두 지역 a, b가 서로 왕복할 수 있음을 의미합니다.(1 ≤ a, b ≤ n, a ≠ b)
   - 동일한 정보가 중복해서 주어지지 않습니다.
     - 동일한 [a, b]가 중복해서 주어지지 않습니다.
     - [a, b]가 있다면 [b, a]는 주어지지 않습니다.
 - 1 ≤ sources의 길이 ≤ 500
   - 1 ≤ sources[i] ≤ n
 - 1 ≤ destination ≤ n

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int n, int[,] roads, int[] sources, int destination) {
        int[] answer = new int[sources.Length];
        int[] distances = new int[n + 1];
        Dictionary<int,List<int>> graph = new Dictionary<int,List<int>>();
        Queue<int> nextRoads = new Queue<int>();
        
        for(int i = 0; i < distances.Length; i++) {
            distances[i] = int.MaxValue;
        }
        
        for(int i = 0; i < roads.GetLength(0); i++) {
            int from = roads[i,0];
            int to = roads[i,1];
            if(!graph.ContainsKey(from)) {
                graph.Add(from, new List<int>());
            }
            if(!graph.ContainsKey(to)) {
                graph.Add(to ,new List<int>());
            }
            graph[from].Add(to);
            graph[to].Add(from);
        }
        
        distances[destination] = 0;
        nextRoads.Enqueue(destination);
        
        while(nextRoads.Count != 0) {
            int current = nextRoads.Dequeue();
            int currentDistance = distances[current];
            
            foreach(int node in graph[current]) {
                int temp = currentDistance + 1;
                if(temp < distances[node]) {
                    distances[node] = temp;
                    nextRoads.Enqueue(node);
                }
            }
        }
        
        for(int i = 0; i < answer.Length; i++) {
            answer[i] = distances[sources[i]];
            if(answer[i] == int.MaxValue) {
                answer[i] = -1;
            }
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.62ms, 31.4MB)
테스트 2 〉	통과 (3.33ms, 31.3MB)
테스트 3 〉	통과 (3.02ms, 31.2MB)
테스트 4 〉	통과 (2.78ms, 31.3MB)
테스트 5 〉	통과 (3.06ms, 31.3MB)
테스트 6 〉	통과 (10.45ms, 35.9MB)
테스트 7 〉	통과 (14.89ms, 40MB)
테스트 8 〉	통과 (14.97ms, 41.2MB)
테스트 9 〉	통과 (7.71ms, 33.7MB)
테스트 10 〉	통과 (8.11ms, 34.3MB)
테스트 11 〉	통과 (389.21ms, 105MB)
테스트 12 〉	통과 (360.61ms, 104MB)
테스트 13 〉	통과 (351.76ms, 104MB)
테스트 14 〉	통과 (399.98ms, 104MB)
테스트 15 〉	통과 (433.45ms, 105MB)
테스트 16 〉	통과 (98.43ms, 59.9MB)
```