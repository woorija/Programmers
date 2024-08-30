# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/138476">귤 고르기</a>

### 문제설명

경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 k와 귤의 크기를 담은 배열 tangerine이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 1 ≤ k ≤ tangerine의 길이 ≤ 100,000
 - 1 ≤ tangerine의 원소 ≤ 10,000,000

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        Dictionary<int,int> counts = new Dictionary<int,int>();
        for(int i = 0; i < tangerine.Length; i++) {
            if(counts.ContainsKey(tangerine[i])) {
                counts[tangerine[i]]++;
            }else{
                counts.Add(tangerine[i],1);
            }
        }
        List<int> tangerines = new List<int>();
        foreach(var dic in counts) {
            tangerines.Add(dic.Value);
        }
        tangerines.Sort();
        tangerines.Reverse();
        int count = 0;
        for(int i = 0; i < tangerines.Count; i++) {
            answer++;
            count += tangerines[i];
            if(count >= k){
                break;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (8.90ms, 33MB)
테스트 2 〉	통과 (9.26ms, 32.6MB)
테스트 3 〉	통과 (9.37ms, 32.8MB)
테스트 4 〉	통과 (14.87ms, 32.8MB)
테스트 5 〉	통과 (9.18ms, 32.5MB)
테스트 6 〉	통과 (9.59ms, 33MB)
테스트 7 〉	통과 (8.95ms, 32.9MB)
테스트 8 〉	통과 (8.92ms, 32.8MB)
테스트 9 〉	통과 (8.95ms, 32.7MB)
테스트 10 〉	통과 (8.89ms, 32.8MB)
테스트 11 〉	통과 (4.05ms, 31.2MB)
테스트 12 〉	통과 (2.51ms, 31.6MB)
테스트 13 〉	통과 (3.62ms, 31MB)
테스트 14 〉	통과 (2.52ms, 31.4MB)
테스트 15 〉	통과 (3.75ms, 31.1MB)
테스트 16 〉	통과 (2.57ms, 31.3MB)
테스트 17 〉	통과 (3.79ms, 31.1MB)
테스트 18 〉	통과 (3.96ms, 31.4MB)
테스트 19 〉	통과 (2.65ms, 31.4MB)
테스트 20 〉	통과 (3.99ms, 31.3MB)
테스트 21 〉	통과 (4.21ms, 31.1MB)
테스트 22 〉	통과 (4.50ms, 31.3MB)
테스트 23 〉	통과 (4.48ms, 31.2MB)
테스트 24 〉	통과 (4.28ms, 31.4MB)
테스트 25 〉	통과 (6.10ms, 31.4MB)
테스트 26 〉	통과 (8.27ms, 33.1MB)
테스트 27 〉	통과 (26.12ms, 39.1MB)
테스트 28 〉	통과 (22.58ms, 35.4MB)
테스트 29 〉	통과 (20.05ms, 35.9MB)
테스트 30 〉	통과 (24.47ms, 38.8MB)
테스트 31 〉	통과 (9.06ms, 32.6MB)
테스트 32 〉	통과 (10.01ms, 33MB)
테스트 33 〉	통과 (23.96ms, 38.7MB)
테스트 34 〉	통과 (19.09ms, 36.2MB)
```