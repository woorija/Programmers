# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/154539">뒤에 있는 큰 수 찾기</a>

### 문제설명

정수로 이루어진 배열 numbers가 있습니다. 배열 의 각 원소들에 대해 자신보다 뒤에 있는 숫자 중에서 자신보다 크면서 가장 가까이 있는 수를 뒷 큰수라고 합니다.
정수 배열 numbers가 매개변수로 주어질 때, 모든 원소에 대한 뒷 큰수들을 차례로 담은 배열을 return 하도록 solution 함수를 완성해주세요. 단, 뒷 큰수가 존재하지 않는 원소는 -1을 담습니다.

***

### 제한사항

 - 4 ≤ numbers의 길이 ≤ 1,000,000
   - 1 ≤ numbers[i] ≤ 1,000,000

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(int[] numbers) {
        int[] answer = new int[numbers.Length];
        answer[answer.Length - 1] = -1;
        for(int i = numbers.Length - 2; i >= 0; i--) {
            for(int j = i + 1; j < numbers.Length; j++) {
                if(numbers[i] < numbers[j]) {
                    answer[i] = numbers[j];
                    break;
                }else{
                    if(answer[j] == -1) {
                        answer[i] = -1;
                            break;
                        }
                    if(numbers[i] < answer[j]) {
                        answer[i] = answer[j];
                        break;
                    }
                }
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.34ms, 31MB)
테스트 2 〉	통과 (0.21ms, 31.3MB)
테스트 3 〉	통과 (0.33ms, 31.1MB)
테스트 4 〉	통과 (0.21ms, 31.4MB)
테스트 5 〉	통과 (0.23ms, 31.7MB)
테스트 6 〉	통과 (0.48ms, 31.7MB)
테스트 7 〉	통과 (0.67ms, 31.7MB)
테스트 8 〉	통과 (2.24ms, 35.1MB)
테스트 9 〉	통과 (2.23ms, 34.9MB)
테스트 10 〉	통과 (3.34ms, 38.8MB)
테스트 11 〉	통과 (3.91ms, 38.8MB)
테스트 12 〉	통과 (6.78ms, 46MB)
테스트 13 〉	통과 (5.50ms, 46.3MB)
테스트 14 〉	통과 (19.54ms, 63.3MB)
테스트 15 〉	통과 (29.62ms, 92.2MB)
테스트 16 〉	통과 (27.57ms, 92.2MB)
테스트 17 〉	통과 (29.76ms, 92.4MB)
테스트 18 〉	통과 (27.29ms, 92.1MB)
테스트 19 〉	통과 (37.16ms, 92.3MB)
테스트 20 〉	통과 (8.00ms, 104MB)
테스트 21 〉	통과 (7.07ms, 84.3MB)
테스트 22 〉	통과 (8.64ms, 81MB)
테스트 23 〉	통과 (6.21ms, 84.6MB)
```