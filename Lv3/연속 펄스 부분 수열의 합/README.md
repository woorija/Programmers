# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/161988">연속 펄스 부분 수열의 합</a>

### 문제설명

어떤 수열의 연속 부분 수열에 같은 길이의 펄스 수열을 각 원소끼리 곱하여 연속 펄스 부분 수열을 만들려 합니다. 펄스 수열이란 [1, -1, 1, -1 …] 또는 [-1, 1, -1, 1 …] 과 같이 1 또는 -1로 시작하면서 1과 -1이 번갈아 나오는 수열입니다.

예를 들어 수열 [2, 3, -6, 1, 3, -1, 2, 4]의 연속 부분 수열 [3, -6, 1]에 펄스 수열 [1, -1, 1]을 곱하면 연속 펄스 부분수열은 [3, 6, 1]이 됩니다. 또 다른 예시로 연속 부분 수열 [3, -1, 2, 4]에 펄스 수열 [-1, 1, -1, 1]을 곱하면 연속 펄스 부분수열은 [-3, -1, -2, 4]이 됩니다.

정수 수열 sequence가 매개변수로 주어질 때, 연속 펄스 부분 수열의 합 중 가장 큰 것을 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ sequence의 길이 ≤ 500,000
 - -100,000 ≤ sequence의 원소 ≤ 100,000
   - sequence의 원소는 정수입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public long solution(int[] sequence) {
        long answer = 0;
        long[] sum1 = new long[sequence.Length + 1];
        long[] sum2 = new long[sequence.Length + 1];
        
        for(int i = 1; i < sequence.Length; i += 2) {
            sequence[i] *= -1;
        }
        
        for(int i = 1; i < sequence.Length + 1; i++) {
            sum1[i] = sum1[i - 1] + sequence[i - 1];
        }
        
        for(int i = 0; i < sequence.Length; i++) {
            sequence[i] *= -1;
        }
        
        for(int i = 1; i < sequence.Length + 1; i++) {
            sum2[i] = sum2[i - 1] + sequence[i - 1];
        }
        
        long max = -50000000000;
        long min = 50000000000;
        
        for(int i = 0; i < sum1.Length; i++) {
            min = Math.Min(min, sum1[i]);
            max = Math.Max(max, sum1[i]);
        }
        answer = max - min;
        
        max = -50000000000;
        min = 50000000000;
        
        for(int i = 0; i < sum2.Length; i++) {
            min = Math.Min(min, sum2[i]);
            max = Math.Max(max, sum2[i]);
        }
        answer = Math.Max(answer, max - min);
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.28ms, 31.2MB)
테스트 2 〉	통과 (0.28ms, 31.1MB)
테스트 3 〉	통과 (0.28ms, 31.3MB)
테스트 4 〉	통과 (0.28ms, 30.9MB)
테스트 5 〉	통과 (0.28ms, 31.3MB)
테스트 6 〉	통과 (0.28ms, 31.2MB)
테스트 7 〉	통과 (0.28ms, 31MB)
테스트 8 〉	통과 (0.30ms, 31.2MB)
테스트 9 〉	통과 (0.31ms, 31.4MB)
테스트 10 〉	통과 (0.38ms, 31.5MB)
테스트 11 〉	통과 (0.48ms, 31.4MB)
테스트 12 〉	통과 (2.27ms, 34.3MB)
테스트 13 〉	통과 (2.28ms, 34.3MB)
테스트 14 〉	통과 (2.28ms, 34.3MB)
테스트 15 〉	통과 (2.26ms, 34.4MB)
테스트 16 〉	통과 (2.32ms, 34.5MB)
테스트 17 〉	통과 (9.64ms, 47.9MB)
테스트 18 〉	통과 (9.46ms, 48.2MB)
테스트 19 〉	통과 (9.78ms, 47.9MB)
테스트 20 〉	통과 (9.78ms, 48MB)
```