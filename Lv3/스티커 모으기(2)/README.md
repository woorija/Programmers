# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12971">스티커 모으기(2)</a>

### 문제설명

N개의 스티커가 원형으로 연결되어 있습니다.

원형으로 연결된 스티커에서 몇 장의 스티커를 뜯어내어 뜯어낸 스티커에 적힌 숫자의 합이 최대가 되도록 하고 싶습니다. 단 스티커 한 장을 뜯어내면 양쪽으로 인접해있는 스티커는 찢어져서 사용할 수 없게 됩니다.

스티커에 적힌 숫자가 배열 형태로 주어질 때, 스티커를 뜯어내어 얻을 수 있는 숫자의 합의 최댓값을 return 하는 solution 함수를 완성해 주세요. 원형의 스티커 모양을 위해 배열의 첫 번째 원소와 마지막 원소가 서로 연결되어 있다고 간주합니다.

***

### 제한사항

 - sticker는 원형으로 연결된 스티커의 각 칸에 적힌 숫자가 순서대로 들어있는 배열로, 길이(N)는 1 이상 100,000 이하입니다.
 - sticker의 각 원소는 스티커의 각 칸에 적힌 숫자이며, 각 칸에 적힌 숫자는 1 이상 100 이하의 자연수입니다.
 - 원형의 스티커 모양을 위해 sticker 배열의 첫 번째 원소와 마지막 원소가 서로 연결되어있다고 간주합니다.

***

### 답안
``` csharp
using System;

class Solution
{
    public int solution(int[] sticker)
    {
        int answer = 0;
        int length = sticker.Length;
        if(length <= 3) {
            for(int i = 0; i < length; i++) {
                answer = Math.Max(answer, sticker[i]);
            }
            return answer;
        }
        
        int[] dp0 = new int[length];
        int[] dp1 = new int[length];
        dp0[0] = sticker[0];
        dp0[1] = sticker[0];
        dp1[0] = 0;
        dp1[1] = sticker[1];
        
        for(int i = 2; i < length - 1; i++) {
            dp1[i] = Math.Max(dp1[i - 1], dp1[i - 2] + sticker[i]);
            dp0[i] = Math.Max(dp0[i - 1],dp0[i - 2] + sticker[i]);
        }
        dp1[length - 1] = Math.Max(dp1[length - 2], dp1[length - 3] + sticker[length - 1]);

        answer = Math.Max(dp0[length - 2], dp1[length - 1]);
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.26ms, 31.5MB)
테스트 2 〉	통과 (0.26ms, 31.3MB)
테스트 3 〉	통과 (0.25ms, 31.5MB)
테스트 4 〉	통과 (0.25ms, 31.4MB)
테스트 5 〉	통과 (0.25ms, 31.3MB)
테스트 6 〉	통과 (0.25ms, 31.4MB)
테스트 7 〉	통과 (0.27ms, 31.6MB)
테스트 8 〉	통과 (0.27ms, 31.4MB)
테스트 9 〉	통과 (0.27ms, 31.5MB)
테스트 10 〉	통과 (0.26ms, 31.2MB)
테스트 11 〉	통과 (0.28ms, 31.1MB)
테스트 12 〉	통과 (0.27ms, 31.5MB)
테스트 13 〉	통과 (0.26ms, 31.3MB)
테스트 14 〉	통과 (0.26ms, 31.2MB)
테스트 15 〉	통과 (0.26ms, 31.5MB)
테스트 16 〉	통과 (0.26ms, 31.4MB)
테스트 17 〉	통과 (0.26ms, 31.5MB)
테스트 18 〉	통과 (0.27ms, 31.3MB)
테스트 19 〉	통과 (0.26ms, 31.4MB)
테스트 20 〉	통과 (0.26ms, 31.5MB)
테스트 21 〉	통과 (0.26ms, 31.5MB)
테스트 22 〉	통과 (0.27ms, 31.5MB)
테스트 23 〉	통과 (0.29ms, 31.6MB)
테스트 24 〉	통과 (0.38ms, 31.3MB)
테스트 25 〉	통과 (0.27ms, 31.5MB)
테스트 26 〉	통과 (0.27ms, 31.4MB)
테스트 27 〉	통과 (0.26ms, 31.5MB)
테스트 28 〉	통과 (0.26ms, 31.5MB)
테스트 29 〉	통과 (0.28ms, 31.4MB)
테스트 30 〉	통과 (0.25ms, 31.5MB)
테스트 31 〉	통과 (0.26ms, 31.5MB)
테스트 32 〉	통과 (0.26ms, 31.6MB)
테스트 33 〉	통과 (0.25ms, 31.2MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (1.01ms, 33.8MB)
테스트 2 〉	통과 (1.06ms, 33.5MB)
테스트 3 〉	통과 (1.10ms, 33.7MB)
테스트 4 〉	통과 (1.11ms, 33.4MB)
```