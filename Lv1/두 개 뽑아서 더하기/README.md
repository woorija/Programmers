# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/68644">두 개 뽑아서 더하기</a>

### 문제설명

정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - numbers의 길이는 2 이상 100 이하입니다.
   - numbers의 모든 수는 0 이상 100 이하입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int[] numbers) {
        List<int> answer = new List<int>();
        
        for(int i = 0; i < numbers.Length - 1; i++) {
            for(int j = i + 1; j < numbers.Length; j++) {
                int temp = numbers[i] + numbers[j];
                if(!answer.Contains(temp)) {
                    answer.Add(temp);
                }
            }
        }
        answer.Sort();
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.17ms, 31.1MB)
테스트 2 〉	통과 (2.38ms, 31.1MB)
테스트 3 〉	통과 (2.37ms, 31.1MB)
테스트 4 〉	통과 (2.14ms, 31MB)
테스트 5 〉	통과 (2.45ms, 31.2MB)
테스트 6 〉	통과 (2.36ms, 31MB)
테스트 7 〉	통과 (3.61ms, 31.4MB)
테스트 8 〉	통과 (2.91ms, 31.2MB)
테스트 9 〉	통과 (1.22ms, 30.9MB)
```