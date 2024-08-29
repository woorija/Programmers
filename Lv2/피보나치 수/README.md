# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12945">피보나치 수</a>

### 문제설명

피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.
예를들어
 - F(2) = F(0) + F(1) = 0 + 1 = 1
 - F(3) = F(1) + F(2) = 1 + 1 = 2
 - F(4) = F(2) + F(3) = 1 + 2 = 3
 - F(5) = F(3) + F(4) = 2 + 3 = 5
와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.

***

### 제한사항

 - n은 2 이상 100,000 이하인 자연수입니다.

***

### 답안
``` csharp
public class Solution {
    public int solution(int n) {
        int answer = 0;
        int prevF1 = 0;
        int prevF2 = 1;
        for(int i = 2;i <= n; i++) {
            answer = prevF1 % 1234567 + prevF2 % 1234567;
            prevF1 = prevF2;
            prevF2 = answer;
        }
        answer = answer % 1234567;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.15ms, 31.4MB)
테스트 2 〉	통과 (0.15ms, 31.3MB)
테스트 3 〉	통과 (0.15ms, 31.4MB)
테스트 4 〉	통과 (0.15ms, 31.3MB)
테스트 5 〉	통과 (0.15ms, 31.4MB)
테스트 6 〉	통과 (0.16ms, 31.5MB)
테스트 7 〉	통과 (0.18ms, 31.5MB)
테스트 8 〉	통과 (0.17ms, 31.2MB)
테스트 9 〉	통과 (0.18ms, 31.4MB)
테스트 10 〉	통과 (0.17ms, 31.6MB)
테스트 11 〉	통과 (0.16ms, 31.4MB)
테스트 12 〉	통과 (0.16ms, 31.5MB)
테스트 13 〉	통과 (1.04ms, 31.2MB)
테스트 14 〉	통과 (1.04ms, 31.3MB)
```