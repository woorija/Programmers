# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12933">정수 내림차순으로 배치하기</a>

### 문제설명

함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 

예를들어 n이 118372면 873211을 리턴하면 됩니다.

***

### 제한사항

 - n은 1이상 8000000000 이하인 자연수입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public long solution(long n) {
        long answer = 0;
        char[] temp = n.ToString().ToCharArray();
        Array.Sort(temp);
        Array.Reverse(temp);
        string aaa = new string(temp);
        answer = long.Parse(aaa);
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.28ms, 31.5MB)
테스트 2 〉	통과 (2.14ms, 31.4MB)
테스트 3 〉	통과 (2.17ms, 31.2MB)
테스트 4 〉	통과 (2.28ms, 31.6MB)
테스트 5 〉	통과 (2.18ms, 31.4MB)
테스트 6 〉	통과 (2.17ms, 31.5MB)
테스트 7 〉	통과 (1.20ms, 31.5MB)
테스트 8 〉	통과 (2.13ms, 31.4MB)
테스트 9 〉	통과 (2.29ms, 31.4MB)
테스트 10 〉	통과 (2.14ms, 31.6MB)
테스트 11 〉	통과 (2.17ms, 31.5MB)
테스트 12 〉	통과 (2.29ms, 31.4MB)
테스트 13 〉	통과 (2.21ms, 31.1MB)
테스트 14 〉	통과 (2.22ms, 31.4MB)
테스트 15 〉	통과 (2.13ms, 31.1MB)
테스트 16 〉	통과 (2.13ms, 31.5MB)
```