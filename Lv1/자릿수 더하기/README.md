# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12931">자릿수 더하기</a>

### 문제설명

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.

예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

***

### 제한사항

 - N의 범위 : 100,000,000 이하의 자연수

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int n) {
        int answer = 0;
        int num = n;
        while(num != 0) {
            answer += num % 10;
            num /= 10;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.18ms, 31.4MB)
테스트 2 〉	통과 (0.14ms, 31.1MB)
테스트 3 〉	통과 (0.15ms, 31.4MB)
테스트 4 〉	통과 (0.15ms, 31.5MB)
테스트 5 〉	통과 (0.15ms, 31.1MB)
테스트 6 〉	통과 (0.17ms, 31.3MB)
테스트 7 〉	통과 (0.15ms, 31.6MB)
테스트 8 〉	통과 (0.15ms, 31.4MB)
테스트 9 〉	통과 (0.15ms, 31.5MB)
테스트 10 〉	통과 (0.15ms, 31.5MB)
테스트 11 〉	통과 (0.15ms, 31.5MB)
테스트 12 〉	통과 (0.15ms, 31.4MB)
테스트 13 〉	통과 (0.15ms, 31MB)
테스트 14 〉	통과 (0.15ms, 31.2MB)
테스트 15 〉	통과 (0.15ms, 31.6MB)
테스트 16 〉	통과 (0.16ms, 31.3MB)
테스트 17 〉	통과 (0.15ms, 31.6MB)
테스트 18 〉	통과 (0.15ms, 31.3MB)
테스트 19 〉	통과 (0.16ms, 31.6MB)
테스트 20 〉	통과 (0.15ms, 31.6MB)
테스트 21 〉	통과 (0.15ms, 31.3MB)
```