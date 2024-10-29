# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/152996">시소 짝꿍</a>

### 문제설명

어느 공원 놀이터에는 시소가 하나 설치되어 있습니다. 이 시소는 중심으로부터 2(m), 3(m), 4(m) 거리의 지점에 좌석이 하나씩 있습니다.

이 시소를 두 명이 마주 보고 탄다고 할 때, 시소가 평형인 상태에서 각각에 의해 시소에 걸리는 토크의 크기가 서로 상쇄되어 완전한 균형을 이룰 수 있다면 그 두 사람을 시소 짝꿍이라고 합니다. 즉, 탑승한 사람의 무게와 시소 축과 좌석 간의 거리의 곱이 양쪽 다 같다면 시소 짝꿍이라고 할 수 있습니다.

사람들의 몸무게 목록 weights이 주어질 때, 시소 짝꿍이 몇 쌍 존재하는지 구하여 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 2 ≤ weights의 길이 ≤ 100,000
 - 100 ≤ weights[i] ≤ 1,000
   - 몸무게 단위는 N(뉴턴)으로 주어집니다.
   - 몸무게는 모두 정수입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public long solution(int[] weights) {
        long answer = 0;
        int[] counts = new int[1001];
        List<int> weightList = new List<int>();
        
        for(int i = 0; i < weights.Length; i++) {
            counts[weights[i]]++;
        }
        
        for(int i = 100; i < counts.Length; i++) {
            long count = counts[i];
            if(count != 0) {
                answer += count * (count - 1) / 2;
                if(i * 2 <= 1000) {
                    answer += count * counts[i * 2];
                }
                if(i * 3 / 2 <= 1000 && i * 3 % 2 == 0) {
                    answer += count * counts[i * 3 / 2];
                }
                if(i * 4 / 3 <= 1000 && i * 4 % 3 == 0) {
                    answer += count * counts[i * 4 / 3];
                }
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.32ms, 31.2MB)
테스트 2 〉	통과 (0.31ms, 31.4MB)
테스트 3 〉	통과 (0.31ms, 31.3MB)
테스트 4 〉	통과 (0.34ms, 31.3MB)
테스트 5 〉	통과 (0.37ms, 31.4MB)
테스트 6 〉	통과 (0.38ms, 31.6MB)
테스트 7 〉	통과 (0.39ms, 31.8MB)
테스트 8 〉	통과 (0.46ms, 32.1MB)
테스트 9 〉	통과 (0.47ms, 32.4MB)
테스트 10 〉	통과 (0.51ms, 32.6MB)
테스트 11 〉	통과 (0.49ms, 32.9MB)
테스트 12 〉	통과 (0.54ms, 32.7MB)
테스트 13 〉	통과 (0.49ms, 33MB)
테스트 14 〉	통과 (0.49ms, 32.8MB)
테스트 15 〉	통과 (0.54ms, 33MB)
테스트 16 〉	통과 (0.31ms, 31.4MB)
테스트 17 〉	통과 (0.32ms, 31.4MB)
```