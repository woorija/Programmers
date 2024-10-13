# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12911">약수의 개수와 덧셈</a>

### 문제설명

두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ left ≤ right ≤ 1,000

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int left, int right) {
        int answer = 0;
        for(int i = left; i <= right; i++) {
            int count = 1;
            for(int j = 1; j < i / 2 + 1; j++) {
                if(i % j == 0) {
                    count++;
                }
            }
            if(count % 2 == 0) {
                answer += i;
            }else{
                answer -= i;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.81ms, 31.5MB)
테스트 2 〉	통과 (0.59ms, 31.4MB)
테스트 3 〉	통과 (0.65ms, 31.3MB)
테스트 4 〉	통과 (0.42ms, 31.5MB)
테스트 5 〉	통과 (1.15ms, 31.5MB)
테스트 6 〉	통과 (0.27ms, 31.5MB)
테스트 7 〉	통과 (0.25ms, 31.4MB)
```