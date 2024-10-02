# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42583">다리를 지나는 트럭</a>

### 문제설명

트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다.

예를 들어, 트럭 2대가 올라갈 수 있고 무게를 10kg까지 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

| 경과 시간 | 다리를 지난 트럭 | 다리를 건너는 트럭 | 대기 트럭 |
| ------- | ------- | ------- | ------- |
| 0 | [] | [] | [7,4,5,6] |
| 1~2 | [] | [7] | [4,5,6] |
| 3 | [7] | [4] | [5,6] |
| 4 | [7] | [4,5] | [6] |
| 5 | [7,4] | [5] | [6] |
| 6~7 | [7,4,5] | [6] | [] |
| 8 | [7,4,5,6] | [] | [] |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

***

### 제한사항

 - bridge_length는 1 이상 10,000 이하입니다.
 - weight는 1 이상 10,000 이하입니다.
 - truck_weights의 길이는 1 이상 10,000 이하입니다.
 - 모든 트럭의 무게는 1 이상 weight 이하입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        int answer = 1;
        List<int> trucks = new List<int>(truck_weights);
        Queue<int> weights = new Queue<int>();
        List<int> times = new List<int>();
        int currentWeight = 0;
        
        while(trucks.Count != 0) {
            answer++;
            for(int i = 0; i < times.Count; i++) {
                times[i]--;
            }
            if(times.Count != 0 && times[0] == 0) {
                currentWeight -= weights.Dequeue();
                times.RemoveAt(0);
            }
            if(weight - currentWeight >= trucks[0]) {
                currentWeight += trucks[0];
                weights.Enqueue(trucks[0]);
                times.Add(bridge_length);
                trucks.RemoveAt(0);
            }
        }
        
        answer += bridge_length - 1;

        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.91ms, 31.3MB)
테스트 2 〉	통과 (3.46ms, 31.4MB)
테스트 3 〉	통과 (1.37ms, 31.4MB)
테스트 4 〉	통과 (5.85ms, 31.3MB)
테스트 5 〉	통과 (35.20ms, 31.8MB)
테스트 6 〉	통과 (24.06ms, 31.5MB)
테스트 7 〉	통과 (2.13ms, 31.2MB)
테스트 8 〉	통과 (1.67ms, 31.5MB)
테스트 9 〉	통과 (2.44ms, 31.4MB)
테스트 10 〉	통과 (1.57ms, 31.3MB)
테스트 11 〉	통과 (1.61ms, 31MB)
테스트 12 〉	통과 (1.90ms, 31.6MB)
테스트 13 〉	통과 (1.46ms, 31.5MB)
테스트 14 〉	통과 (1.44ms, 31.5MB)
```