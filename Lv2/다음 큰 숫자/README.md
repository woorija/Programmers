# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12911">다음 큰 숫자</a>

### 문제설명

자연수 n이 주어졌을 때, n의 다음 큰 숫자는 다음과 같이 정의 합니다.

 - 조건 1. n의 다음 큰 숫자는 n보다 큰 자연수 입니다.
 - 조건 2. n의 다음 큰 숫자와 n은 2진수로 변환했을 때 1의 갯수가 같습니다.
 - 조건 3. n의 다음 큰 숫자는 조건 1, 2를 만족하는 수 중 가장 작은 수 입니다.
예를 들어서 78(1001110)의 다음 큰 숫자는 83(1010011)입니다.

자연수 n이 매개변수로 주어질 때, n의 다음 큰 숫자를 return 하는 solution 함수를 완성해주세요.

***

### 제한사항

 - n은 1,000,000 이하의 자연수 입니다.

***

### 답안
``` csharp
using System;

class Solution {
    public int solution(int n) {
        int answer = n+1;
        string str1 = Convert.ToString(n,2);
        int count = 0;
        for(int i = 0; i < str1.Length; i++) {
            if(str1[i] == '1') {
                count++;
            }
        }
        int answerCount;
        string str2;
        while(true) {
            str2 = Convert.ToString(answer, 2);
            answerCount = 0;
            for(int i = 0; i < str2.Length; i++) {
                if(str2[i] == '1') {
                      answerCount++;
                 }
            }
            if(count == answerCount) {
                break;
            }
            answer++;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.34ms, 31.2MB)
테스트 2 〉	통과 (0.35ms, 31.6MB)
테스트 3 〉	통과 (0.49ms, 31.5MB)
테스트 4 〉	통과 (0.38ms, 31.1MB)
테스트 5 〉	통과 (0.37ms, 30.7MB)
테스트 6 〉	통과 (0.29ms, 31.3MB)
테스트 7 〉	통과 (0.30ms, 30.9MB)
테스트 8 〉	통과 (0.49ms, 31MB)
테스트 9 〉	통과 (0.32ms, 31.3MB)
테스트 10 〉	통과 (0.50ms, 31.2MB)
테스트 11 〉	통과 (0.31ms, 31.1MB)
테스트 12 〉	통과 (0.31ms, 31.1MB)
테스트 13 〉	통과 (0.31ms, 31.1MB)
테스트 14 〉	통과 (0.33ms, 31.4MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (0.29ms, 30.9MB)
테스트 2 〉	통과 (0.28ms, 31.3MB)
테스트 3 〉	통과 (0.28ms, 31.2MB)
테스트 4 〉	통과 (0.28ms, 30.9MB)
테스트 5 〉	통과 (0.30ms, 31.2MB)
테스트 6 〉	통과 (0.28ms, 31.1MB)
```