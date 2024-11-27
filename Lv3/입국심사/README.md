# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43238">입국심사</a>

### 문제설명

n명이 입국심사를 위해 줄을 서서 기다리고 있습니다. 각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다. 가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다. 하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
 - 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
 - 심사관은 1명 이상 100,000명 이하입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public long solution(int n, int[] times) {
        long answer = 0;
        long min = 0;
        long max = 0;
        for(int i = 0; i < times.Length; i++) {
            if(max < times[i]) {
                max = times[i];
            }
        }
        max *= n;
        
        while(min != max) {
            long mid = (max + min) / 2;
            long count = 0;
            
            for(int i = 0; i < times.Length; i++) {
                count += mid / times[i];
            }
            
            if(count >= n) {
                max = mid;
            }else{
                min = mid + 1;
            }
        }

        return min;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.20ms, 31.3MB)
테스트 2 〉	통과 (0.21ms, 31.3MB)
테스트 3 〉	통과 (0.56ms, 31MB)
테스트 4 〉	통과 (39.95ms, 32.8MB)
테스트 5 〉	통과 (40.62ms, 32.9MB)
테스트 6 〉	통과 (36.45ms, 32.7MB)
테스트 7 〉	통과 (50.73ms, 32.7MB)
테스트 8 〉	통과 (50.69ms, 32.9MB)
테스트 9 〉	통과 (0.20ms, 31.4MB)
```