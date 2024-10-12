# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12932">자연수 뒤집어 배열로 만들기</a>

### 문제설명

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

***

### 제한사항

 - n은 10,000,000,000이하인 자연수입니다.

***

### 답안
``` csharp
using System.Collections.Generic;

public class Solution {
    public int[] solution(long n) {
        int temp;
        List<int> answer = new List<int>();
        int i = 0;
        while(n > 0){
            temp = (int)(n % 10);
            answer.Add(temp);
            n /= 10;
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.48ms, 31.2MB)
테스트 2 〉	통과 (0.49ms, 30.9MB)
테스트 3 〉	통과 (0.54ms, 31MB)
테스트 4 〉	통과 (0.49ms, 31.5MB)
테스트 5 〉	통과 (0.51ms, 31.4MB)
테스트 6 〉	통과 (0.49ms, 31.1MB)
테스트 7 〉	통과 (0.48ms, 31.3MB)
테스트 8 〉	통과 (0.53ms, 31.1MB)
테스트 9 〉	통과 (0.51ms, 31MB)
테스트 10 〉	통과 (0.48ms, 31.1MB)
테스트 11 〉	통과 (0.51ms, 31.4MB)
테스트 12 〉	통과 (0.50ms, 31.3MB)
테스트 13 〉	통과 (0.52ms, 31.1MB)
```