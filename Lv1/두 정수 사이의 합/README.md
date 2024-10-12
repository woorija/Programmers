# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12912">두 정수 사이의 합</a>

### 문제설명

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.

예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.

***

### 제한사항

 - a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
 - a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
 - a와 b의 대소관계는 정해져있지 않습니다.

***

### 답안
``` csharp
public class Solution {
    public long solution(int a, int b) {
        long answer = 0;
        int tempA = 0;
        int tempB = 0;
        
        if(a == b) {
            return a;
        }
        if(b > a) {
            tempA = a;
            tempB = b;
        }else{
            tempA = b;
            tempB = a;
        }
        for(int i = tempA; i <= tempB; i++) {
            answer += i;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.16ms, 31MB)
테스트 2 〉	통과 (0.16ms, 31.4MB)
테스트 3 〉	통과 (0.16ms, 31.4MB)
테스트 4 〉	통과 (20.20ms, 31.3MB)
테스트 5 〉	통과 (13.87ms, 31.2MB)
테스트 6 〉	통과 (12.07ms, 31.6MB)
테스트 7 〉	통과 (5.23ms, 31.3MB)
테스트 8 〉	통과 (9.45ms, 31.3MB)
테스트 9 〉	통과 (6.99ms, 31.3MB)
테스트 10 〉	통과 (1.62ms, 31.5MB)
테스트 11 〉	통과 (0.16ms, 31.2MB)
테스트 12 〉	통과 (0.17ms, 31.4MB)
테스트 13 〉	통과 (0.16ms, 31.2MB)
테스트 14 〉	통과 (0.17ms, 31.4MB)
테스트 15 〉	통과 (0.17ms, 31.3MB)
테스트 16 〉	통과 (0.17ms, 31.2MB)
```