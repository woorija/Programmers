# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/70128">내적</a>

### 문제설명

길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.

이때, a와 b의 내적은 a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1] 입니다. (n은 a, b의 길이)

***

### 제한사항

 - a, b의 길이는 1 이상 1,000 이하입니다.
 - a, b의 모든 수는 -1,000 이상 1,000 이하입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int[] a, int[] b) {
        int answer = 0;
        for(int i = 0; i < a.Length; i++) {
            answer += a[i] * b[i];
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.16ms, 31.5MB)
테스트 2 〉	통과 (0.16ms, 31.2MB)
테스트 3 〉	통과 (0.16ms, 31.6MB)
테스트 4 〉	통과 (0.16ms, 31.5MB)
테스트 5 〉	통과 (0.16ms, 31.4MB)
테스트 6 〉	통과 (0.16ms, 31.4MB)
테스트 7 〉	통과 (0.16ms, 31.5MB)
테스트 8 〉	통과 (0.18ms, 31.4MB)
```