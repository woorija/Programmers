# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/178870">연속된 부분 수열의 합</a>

### 문제설명

비내림차순으로 정렬된 수열이 주어질 때, 다음 조건을 만족하는 부분 수열을 찾으려고 합니다.

 - 기존 수열에서 임의의 두 인덱스의 원소와 그 사이의 원소를 모두 포함하는 부분 수열이어야 합니다.
 - 부분 수열의 합은 k입니다.
 - 합이 k인 부분 수열이 여러 개인 경우 길이가 짧은 수열을 찾습니다.
 - 길이가 짧은 수열이 여러 개인 경우 앞쪽(시작 인덱스가 작은)에 나오는 수열을 찾습니다.

수열을 나타내는 정수 배열 sequence와 부분 수열의 합을 나타내는 정수 k가 매개변수로 주어질 때, 위 조건을 만족하는 부분 수열의 시작 인덱스와 마지막 인덱스를 배열에 담아 return 하는 solution 함수를 완성해주세요. 이때 수열의 인덱스는 0부터 시작합니다.

***

### 제한사항

 - 5 ≤ sequence의 길이 ≤ 1,000,000
   - 1 ≤ sequence의 원소 ≤ 1,000
   - sequence는 비내림차순으로 정렬되어 있습니다.
 - 5 ≤ k ≤ 1,000,000,000
   - k는 항상 sequence의 부분 수열로 만들 수 있는 값입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(int[] sequence, int k) {
        int first = sequence.Length - 1;
        int last = sequence.Length - 1;
        int sum = sequence[last];
        
        while(sum != k) {
            if(sum < k) {
                first--;
                sum += sequence[first];
            }else{
                sum -= sequence[last];
                last--;
            }
        }
        while(sum == k) {
            if(first != 0) {
            first--;
            sum += sequence[first];
            sum -= sequence[last];
            last--;
            }else{
                break;
            }
        }
        if(sum != k) {
            first++;
            last++;
        }
        int[] answer = new int[2] { first, last };
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.20ms, 31.2MB)
테스트 2 〉	통과 (0.21ms, 31.5MB)
테스트 3 〉	통과 (0.24ms, 31.2MB)
테스트 4 〉	통과 (0.23ms, 31.3MB)
테스트 5 〉	통과 (0.20ms, 31.6MB)
테스트 6 〉	통과 (0.22ms, 31.2MB)
테스트 7 〉	통과 (0.22ms, 31.8MB)
테스트 8 〉	통과 (0.20ms, 32.6MB)
테스트 9 〉	통과 (0.22ms, 34.3MB)
테스트 10 〉	통과 (0.28ms, 40.2MB)
테스트 11 〉	통과 (0.92ms, 50MB)
테스트 12 〉	통과 (0.67ms, 49.8MB)
테스트 13 〉	통과 (0.56ms, 50MB)
테스트 14 〉	통과 (0.53ms, 49.9MB)
테스트 15 〉	통과 (0.48ms, 50MB)
테스트 16 〉	통과 (1.97ms, 49.8MB)
테스트 17 〉	통과 (1.75ms, 50.1MB)
테스트 18 〉	통과 (0.21ms, 31.4MB)
테스트 19 〉	통과 (0.22ms, 31.5MB)
테스트 20 〉	통과 (0.23ms, 31.1MB)
테스트 21 〉	통과 (0.20ms, 31.2MB)
테스트 22 〉	통과 (0.20ms, 31.4MB)
테스트 23 〉	통과 (0.20ms, 31.2MB)
테스트 24 〉	통과 (1.84ms, 50.2MB)
테스트 25 〉	통과 (2.00ms, 50MB)
테스트 26 〉	통과 (3.49ms, 50.1MB)
테스트 27 〉	통과 (0.31ms, 50.1MB)
테스트 28 〉	통과 (2.89ms, 50.1MB)
테스트 29 〉	통과 (1.12ms, 50.1MB)
테스트 30 〉	통과 (3.41ms, 49.5MB)
테스트 31 〉	통과 (0.20ms, 31.1MB)
테스트 32 〉	통과 (0.20ms, 31.5MB)
테스트 33 〉	통과 (0.22ms, 31.4MB)
테스트 34 〉	통과 (0.21ms, 31.3MB)
```