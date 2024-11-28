# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42862">체육복</a>

### 문제설명

점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 전체 학생의 수는 2명 이상 30명 이하입니다.
 - 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
 - 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
 - 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
 - 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        Array.Sort(lost);
        List<int> reserves = new List<int>(reserve);
        int answer = n - lost.Length;
        
        for(int i = 0; i < lost.Length; i++) {
            if(reserves.Contains(lost[i])) {
                reserves.Remove(lost[i]);
                answer++;
                lost[i] = -1;
            }
        }
        
        for(int i = 0; i < lost.Length; i++) {
            for(int j = -1; j <= 1; j += 2) {
                int temp = lost[i] + j;
                if(reserves.Contains(temp)) {
                    lost[i] = -1;
                    answer++;
                    reserves.Remove(temp);
                    break;
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
테스트 1 〉	통과 (3.09ms, 31MB)
테스트 2 〉	통과 (3.80ms, 30.8MB)
테스트 3 〉	통과 (3.54ms, 31MB)
테스트 4 〉	통과 (2.51ms, 31.1MB)
테스트 5 〉	통과 (3.37ms, 31.1MB)
테스트 6 〉	통과 (2.31ms, 31.1MB)
테스트 7 〉	통과 (2.27ms, 31.1MB)
테스트 8 〉	통과 (2.30ms, 31.1MB)
테스트 9 〉	통과 (2.34ms, 31MB)
테스트 10 〉	통과 (2.69ms, 31MB)
테스트 11 〉	통과 (2.39ms, 31MB)
테스트 12 〉	통과 (2.49ms, 31.1MB)
테스트 13 〉	통과 (2.36ms, 30.9MB)
테스트 14 〉	통과 (2.67ms, 31.1MB)
테스트 15 〉	통과 (2.54ms, 31.1MB)
테스트 16 〉	통과 (2.45ms, 31MB)
테스트 17 〉	통과 (2.32ms, 31.2MB)
테스트 18 〉	통과 (2.64ms, 31.1MB)
테스트 19 〉	통과 (3.80ms, 31.3MB)
테스트 20 〉	통과 (2.31ms, 31MB)
테스트 21 〉	통과 (1.48ms, 31.2MB)
테스트 22 〉	통과 (1.28ms, 31.2MB)
테스트 23 〉	통과 (1.23ms, 31MB)
테스트 24 〉	통과 (2.54ms, 31.3MB)
테스트 25 〉	통과 (2.31ms, 31.3MB)
테스트 26 〉	통과 (2.34ms, 31MB)
테스트 27 〉	통과 (2.36ms, 31MB)
테스트 28 〉	통과 (2.68ms, 31.1MB)
테스트 29 〉	통과 (2.91ms, 30.7MB)
테스트 30 〉	통과 (3.19ms, 30.9MB)
```