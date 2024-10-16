# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12921">소수 찾기</a>

### 문제설명

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.

(1은 소수가 아닙니다.)

***

### 제한사항

 - n은 2이상 1000000이하의 자연수입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int n) {
        int answer=0;
        bool[] isPrime = new bool[n + 1];
        
        for(int i = 2; i < isPrime.Length; i++) {
            isPrime[i] = true;
        }
        
        for(int i = 2; i <= Math.Sqrt(n); i++) {
            int j = 2;
            if(isPrime[i]) {
                while(i * j <= n) {
                    isPrime[i * j] = false;
                    j++;
                }
            }
        }
        
        for(int i = 2; i < isPrime.Length; i++) {
            if(isPrime[i]) {
                answer++;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.23ms, 31.3MB)
테스트 2 〉	통과 (0.23ms, 31.7MB)
테스트 3 〉	통과 (0.22ms, 31.6MB)
테스트 4 〉	통과 (0.24ms, 31.1MB)
테스트 5 〉	통과 (0.22ms, 31.5MB)
테스트 6 〉	통과 (0.30ms, 31.5MB)
테스트 7 〉	통과 (0.33ms, 31.3MB)
테스트 8 〉	통과 (0.32ms, 31.4MB)
테스트 9 〉	통과 (0.34ms, 31.5MB)
테스트 10 〉	통과 (2.15ms, 31.6MB)
테스트 11 〉	통과 (9.74ms, 31.9MB)
테스트 12 〉	통과 (2.62ms, 31.6MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (6.11ms, 31.8MB)
테스트 2 〉	통과 (6.33ms, 31.9MB)
테스트 3 〉	통과 (6.22ms, 31.9MB)
테스트 4 〉	통과 (6.30ms, 31.8MB)
```