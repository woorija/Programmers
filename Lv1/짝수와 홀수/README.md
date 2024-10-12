# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12937">짝수와 홀수</a>

### 문제설명

정수 num이 짝수일 경우 "Even"을 반환하고 홀수인 경우 "Odd"를 반환하는 함수, solution을 완성해주세요.

***

### 제한사항

 - num은 int 범위의 정수입니다.
 - 0은 짝수입니다.

***

### 답안
``` csharp
public class Solution {
    public string solution(int num) {
        if(num % 2 == 0) {
            return "Even";
        }
        return "Odd";
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.13ms, 31MB)
테스트 2 〉	통과 (0.14ms, 31.2MB)
테스트 3 〉	통과 (0.14ms, 31.1MB)
테스트 4 〉	통과 (0.13ms, 31.3MB)
테스트 5 〉	통과 (0.14ms, 31MB)
테스트 6 〉	통과 (0.14ms, 31.1MB)
테스트 7 〉	통과 (0.14ms, 31.2MB)
테스트 8 〉	통과 (0.13ms, 31MB)
테스트 9 〉	통과 (0.13ms, 30.8MB)
테스트 10 〉	통과 (0.13ms, 31.3MB)
테스트 11 〉	통과 (0.13ms, 31.1MB)
테스트 12 〉	통과 (0.13ms, 30.8MB)
테스트 13 〉	통과 (0.13ms, 31.2MB)
테스트 14 〉	통과 (0.13ms, 31.2MB)
테스트 15 〉	통과 (0.14ms, 31.3MB)
테스트 16 〉	통과 (0.14ms, 31MB)
```