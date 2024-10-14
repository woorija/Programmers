# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/68935">3진법 뒤집기</a>

### 문제설명

자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - n은 1 이상 100,000,000 이하인 자연수입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int n) {
        List<char> list = new List<char>();
        int answer = 0;
        int num = n;
        while(num != 0) {
            list.Add((char)((num % 3) + '0'));
            num /= 3;
        }
        string str = new string(list.ToArray());

        long reverse = long.Parse(str);
        int value = 1;
        
        while(reverse != 0) {
            answer += value * (int)(reverse % 10);
            value *= 3;
            reverse /= 10;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.17ms, 31.3MB)
테스트 2 〉	통과 (1.16ms, 31.4MB)
테스트 3 〉	통과 (1.17ms, 31.5MB)
테스트 4 〉	통과 (1.32ms, 31.4MB)
테스트 5 〉	통과 (1.18ms, 31.1MB)
테스트 6 〉	통과 (1.13ms, 31.4MB)
테스트 7 〉	통과 (1.15ms, 31.4MB)
테스트 8 〉	통과 (2.57ms, 31.5MB)
테스트 9 〉	통과 (1.10ms, 31.3MB)
테스트 10 〉	통과 (1.29ms, 31.5MB)
```