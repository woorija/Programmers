# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12928">약수의 합</a>

### 문제설명

정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요.

***

### 제한사항

 - n은 0 이상 3000이하인 정수입니다.

***

### 답안
``` csharp
public class Solution {
    public int solution(int n) {
        int answer = 0;
        for(int i = 1; i < n / 2 + 1; i++) {
            if(n % i == 0) {
                answer += i;
            }
        }
        answer += n;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.15ms, 31.4MB)
테스트 2 〉	통과 (0.15ms, 31.3MB)
테스트 3 〉	통과 (0.15ms, 31.2MB)
테스트 4 〉	통과 (0.15ms, 31MB)
테스트 5 〉	통과 (0.15ms, 31MB)
테스트 6 〉	통과 (0.15ms, 31.3MB)
테스트 7 〉	통과 (0.17ms, 31.1MB)
테스트 8 〉	통과 (0.16ms, 30.9MB)
테스트 9 〉	통과 (0.16ms, 31.3MB)
테스트 10 〉	통과 (0.16ms, 31.5MB)
테스트 11 〉	통과 (0.16ms, 31.4MB)
테스트 12 〉	통과 (0.16ms, 31.4MB)
테스트 13 〉	통과 (0.16ms, 31.6MB)
테스트 14 〉	통과 (0.17ms, 31.1MB)
테스트 15 〉	통과 (0.16ms, 31.3MB)
테스트 16 〉	통과 (0.17ms, 31.2MB)
테스트 17 〉	통과 (0.18ms, 31.6MB)
```