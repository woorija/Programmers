# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87389">나머지가 1이 되는 수 찾기</a>

### 문제설명

자연수 n이 매개변수로 주어집니다. n을 x로 나눈 나머지가 1이 되도록 하는 가장 작은 자연수 x를 return 하도록 solution 함수를 완성해주세요. 답이 항상 존재함은 증명될 수 있습니다.

***

### 제한사항

 - 3 ≤ n ≤ 1,000,000

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = n - 1; i > 0; i--) {
            if(n % i == 1) {
                answer = i;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.51ms, 31.2MB)
테스트 2 〉	통과 (0.41ms, 31.3MB)
테스트 3 〉	통과 (3.11ms, 31.1MB)
테스트 4 〉	통과 (3.51ms, 30.9MB)
테스트 5 〉	통과 (0.15ms, 31.3MB)
테스트 6 〉	통과 (0.15ms, 31.5MB)
테스트 7 〉	통과 (0.15ms, 31.4MB)
테스트 8 〉	통과 (0.16ms, 31MB)
테스트 9 〉	통과 (0.26ms, 31.4MB)
테스트 10 〉	통과 (1.43ms, 31.4MB)
테스트 11 〉	통과 (2.57ms, 31.1MB)
```