# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42584">주식가격</a>

### 문제설명

초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

***

### 제한사항

 - prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
 - prices의 길이는 2 이상 100,000 이하입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.Length];
        for(int i = 0; i < prices.Length; i++) {
            answer[i] = answer.Length - 1 - i;
            int count = 0;
            for(int j = i + 1; j < prices.Length; j++) {
                count++;
                if(prices[i] > prices[j]) {
                    answer[i] = count;
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
테스트 1 〉	통과 (0.18ms, 31.4MB)
테스트 2 〉	통과 (0.20ms, 31.3MB)
테스트 3 〉	통과 (0.21ms, 31.4MB)
테스트 4 〉	통과 (0.21ms, 31.5MB)
테스트 5 〉	통과 (0.27ms, 31.7MB)
테스트 6 〉	통과 (0.18ms, 31.5MB)
테스트 7 〉	통과 (0.22ms, 31.5MB)
테스트 8 〉	통과 (0.20ms, 31.4MB)
테스트 9 〉	통과 (0.29ms, 31.4MB)
테스트 10 〉	통과 (0.23ms, 31.5MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (3.06ms, 36.9MB)
테스트 2 〉	통과 (2.43ms, 35.5MB)
테스트 3 〉	통과 (3.68ms, 37.7MB)
테스트 4 〉	통과 (2.83ms, 35.8MB)
테스트 5 〉	통과 (1.86ms, 34.9MB)
```