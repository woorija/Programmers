# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12910">나누어 떨어지는 숫자 배열</a>

### 문제설명

array의 각 element 중 divisor로 나누어 떨어지는 값을 오름차순으로 정렬한 배열을 반환하는 함수, solution을 작성해주세요.

divisor로 나누어 떨어지는 element가 하나도 없다면 배열에 -1을 담아 반환하세요.

***

### 제한사항

 - arr은 자연수를 담은 배열입니다.
 - 정수 i, j에 대해 i ≠ j 이면 arr[i] ≠ arr[j] 입니다.
 - divisor는 자연수입니다.
 - array는 길이 1 이상인 배열입니다.

***

### 답안
``` csharp
using System.Collections.Generic;

public class Solution {
    public int[] solution(int[] arr, int divisor) {
        List<int> answer = new List<int>();
        
        for(int i = 0; i < arr.Length; i++) {
            if(arr[i] % divisor == 0) {
                answer.Add(arr[i]);
            }
        }
        if(answer.Count != 0) {
            answer.Sort();
        }else{
            answer.Add(-1);
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.88ms, 31.5MB)
테스트 2 〉	통과 (2.52ms, 31MB)
테스트 3 〉	통과 (2.16ms, 30.8MB)
테스트 4 〉	통과 (1.81ms, 31.2MB)
테스트 5 〉	통과 (2.02ms, 30.9MB)
테스트 6 〉	통과 (0.88ms, 32.2MB)
테스트 7 〉	통과 (0.65ms, 31.3MB)
테스트 8 〉	통과 (0.59ms, 31.1MB)
테스트 9 〉	통과 (0.72ms, 31.3MB)
테스트 10 〉	통과 (3.10ms, 31.1MB)
테스트 11 〉	통과 (2.08ms, 31.4MB)
테스트 12 〉	통과 (1.86ms, 31.3MB)
테스트 13 〉	통과 (0.58ms, 31.1MB)
테스트 14 〉	통과 (1.98ms, 31.1MB)
테스트 15 〉	통과 (2.12ms, 31.4MB)
테스트 16 〉	통과 (2.11ms, 31.2MB)
```