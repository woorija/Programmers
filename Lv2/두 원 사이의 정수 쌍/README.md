# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/181187">두 원 사이의 정수 쌍</a>

### 문제설명

x축과 y축으로 이루어진 2차원 직교 좌표계에 중심이 원점인 서로 다른 크기의 원이 두 개 주어집니다. 반지름을 나타내는 두 정수 r1, r2가 매개변수로 주어질 때, 두 원 사이의 공간에 x좌표와 y좌표가 모두 정수인 점의 개수를 return하도록 solution 함수를 완성해주세요.

※ 각 원 위의 점도 포함하여 셉니다.

***

### 제한사항

 - 1 ≤ r1 < r2 ≤ 1,000,000

***

### 답안
``` csharp
using System;

public class Solution {
    public long solution(int r1, int r2) {
        long answer = 0;
        long maxR2 = (long)r2 * r2;
        long maxR1 = (long)r1 * r1;
        for(long i = 1; i <= r2; i++) {
            answer += (long)Math.Sqrt(maxR2 - i * i) - (long)Math.Ceiling((double)Math.Sqrt(maxR1 - i * i)) + 1;
        }
        answer *= 4;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.26ms, 31.5MB)
테스트 2 〉	통과 (0.27ms, 31.4MB)
테스트 3 〉	통과 (0.27ms, 31.4MB)
테스트 4 〉	통과 (0.46ms, 31.6MB)
테스트 5 〉	통과 (0.38ms, 31.4MB)
테스트 6 〉	통과 (0.50ms, 31.5MB)
테스트 7 〉	통과 (66.65ms, 31.5MB)
테스트 8 〉	통과 (60.48ms, 31.4MB)
테스트 9 〉	통과 (48.24ms, 31.5MB)
테스트 10 〉	통과 (118.10ms, 31.2MB)
```