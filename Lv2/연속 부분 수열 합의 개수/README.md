# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/131701">연속 부분 수열 합의 개수</a>

### 문제설명

철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.

원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.
원형 수열의 모든 원소 elements가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 3 ≤ elements의 길이 ≤ 1,000
 - 1 ≤ elements의 원소 ≤ 1,000

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int[] elements) {
        HashSet<int> count = new HashSet<int>();
        int length = elements.Length;
        int temp = 0;
        for(int i = 0; i < length; i++) {
            temp = 0;
            for(int j = i; j < length + i; j++) {
                temp += elements[j % length];
                count.Add(temp);
            }
        }
        
        return count.Count;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.06ms, 31.1MB)
테스트 2 〉	통과 (3.54ms, 31.9MB)
테스트 3 〉	통과 (9.46ms, 32.9MB)
테스트 4 〉	통과 (11.45ms, 35.2MB)
테스트 5 〉	통과 (20.54ms, 38.3MB)
테스트 6 〉	통과 (24.14ms, 38.9MB)
테스트 7 〉	통과 (30.54ms, 39.6MB)
테스트 8 〉	통과 (45.37ms, 40.2MB)
테스트 9 〉	통과 (62.11ms, 46.2MB)
테스트 10 〉	통과 (77.64ms, 47.2MB)
테스트 11 〉	통과 (21.85ms, 38.6MB)
테스트 12 〉	통과 (26.17ms, 39MB)
테스트 13 〉	통과 (28.76ms, 39.5MB)
테스트 14 〉	통과 (46.06ms, 39.8MB)
테스트 15 〉	통과 (42.25ms, 39.9MB)
테스트 16 〉	통과 (45.34ms, 40.4MB)
테스트 17 〉	통과 (57.41ms, 46MB)
테스트 18 〉	통과 (65.79ms, 46.3MB)
테스트 19 〉	통과 (89.15ms, 46.8MB)
테스트 20 〉	통과 (65.43ms, 47.1MB)
```