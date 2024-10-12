# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/86051">없는 숫자 더하기</a>

### 문제설명

0부터 9까지의 숫자 중 일부가 들어있는 정수 배열 numbers가 매개변수로 주어집니다. 

numbers에서 찾을 수 없는 0부터 9까지의 숫자를 모두 찾아 더한 수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ numbers의 길이 ≤ 9
   - 0 ≤ numbers의 모든 원소 ≤ 9
   - numbers의 모든 원소는 서로 다릅니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int[] numbers) {
        int answer = 45;
        for(int i = 0; i < numbers.Length; i++) {
            answer -= numbers[i];
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.15ms, 31.2MB)
테스트 2 〉	통과 (0.17ms, 31.4MB)
테스트 3 〉	통과 (0.16ms, 31.3MB)
테스트 4 〉	통과 (0.17ms, 31.3MB)
테스트 5 〉	통과 (0.16ms, 31.4MB)
테스트 6 〉	통과 (0.15ms, 31.3MB)
테스트 7 〉	통과 (0.15ms, 31.2MB)
테스트 8 〉	통과 (0.16ms, 31.3MB)
```