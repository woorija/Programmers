# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12954">x만큼 간격이 있는 n개의 숫자</a>

### 문제설명

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.

***

### 제한사항

 - x는 -10000000 이상, 10000000 이하인 정수입니다.
 - n은 1000 이하인 자연수입니다.

***

### 답안
``` csharp
using System.Collections.Generic;

public class Solution {
    List<long> answer = new List<long>();
    public long[] solution(int x, int n) {
        for(long i = 1; i <= n; i++) {
            answer.Add(x * i);
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.43ms, 31.1MB)
테스트 2 〉	통과 (0.42ms, 31.1MB)
테스트 3 〉	통과 (0.42ms, 31.1MB)
테스트 4 〉	통과 (0.45ms, 31.1MB)
테스트 5 〉	통과 (0.47ms, 31.2MB)
테스트 6 〉	통과 (0.41ms, 31.2MB)
테스트 7 〉	통과 (0.46ms, 31.4MB)
테스트 8 〉	통과 (0.42ms, 31.4MB)
테스트 9 〉	통과 (0.44ms, 31.5MB)
테스트 10 〉	통과 (0.43ms, 31.1MB)
테스트 11 〉	통과 (0.42ms, 31.4MB)
테스트 12 〉	통과 (0.46ms, 31.5MB)
테스트 13 〉	통과 (0.46ms, 31.3MB)
```