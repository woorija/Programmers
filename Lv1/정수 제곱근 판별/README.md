# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12934">정수 제곱근 판별</a>

### 문제설명

임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.

n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

***

### 제한사항

 - n은 1이상, 50000000000000 이하인 양의 정수입니다.

***

### 답안
``` csharp
public class Solution {
    public long solution(long n) {
        long answer = -1;
        long temp = -1;
        for(long i = 1; i <= 10000000; i++) {
            if(i * i == n){
                temp = i;
                break;
            }
        }
        if(temp != -1) {
            temp += 1;
            answer = temp * temp;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (13.80ms, 31.2MB)
테스트 2 〉	통과 (9.15ms, 31.3MB)
테스트 3 〉	통과 (13.03ms, 31.2MB)
테스트 4 〉	통과 (1.92ms, 31MB)
테스트 5 〉	통과 (0.18ms, 31.1MB)
테스트 6 〉	통과 (13.91ms, 31.2MB)
테스트 7 〉	통과 (0.24ms, 31.2MB)
테스트 8 〉	통과 (0.18ms, 31MB)
테스트 9 〉	통과 (0.18ms, 31.3MB)
테스트 10 〉	통과 (0.24ms, 31.3MB)
테스트 11 〉	통과 (0.27ms, 31.5MB)
테스트 12 〉	통과 (0.24ms, 31.2MB)
테스트 13 〉	통과 (14.19ms, 31MB)
테스트 14 〉	통과 (0.28ms, 31.3MB)
테스트 15 〉	통과 (0.18ms, 31.2MB)
테스트 16 〉	통과 (0.17ms, 31.1MB)
테스트 17 〉	통과 (0.16ms, 31.5MB)
테스트 18 〉	통과 (0.16ms, 31MB)
```