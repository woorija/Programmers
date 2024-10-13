# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/82612">부족한 금액 계산하기</a>

### 문제설명

새로 생긴 놀이기구는 인기가 매우 많아 줄이 끊이질 않습니다. 이 놀이기구의 원래 이용료는 price원 인데, 놀이기구를 N 번 째 이용한다면 원래 이용료의 N배를 받기로 하였습니다. 즉, 처음 이용료가 100이었다면 2번째에는 200, 3번째에는 300으로 요금이 인상됩니다.

놀이기구를 count번 타게 되면 현재 자신이 가지고 있는 금액에서 얼마가 모자라는지를 return 하도록 solution 함수를 완성하세요.

단, 금액이 부족하지 않으면 0을 return 하세요.

***

### 제한사항

 - 놀이기구의 이용료 price : 1 ≤ price ≤ 2,500, price는 자연수
 - 처음 가지고 있던 금액 money : 1 ≤ money ≤ 1,000,000,000, money는 자연수
 - 놀이기구의 이용 횟수 count : 1 ≤ count ≤ 2,500, count는 자연수

***

### 답안
``` csharp
using System;

class Solution
{
    public long solution(int price, int money, int count)
    {
        long answer = (price + (long)(price * count)) * count / 2 - money;
        
        return Math.Max(0, answer);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.15ms, 31.5MB)
테스트 2 〉	통과 (0.15ms, 31.3MB)
테스트 3 〉	통과 (0.16ms, 31.1MB)
테스트 4 〉	통과 (0.15ms, 31.5MB)
테스트 5 〉	통과 (0.24ms, 31.4MB)
테스트 6 〉	통과 (0.17ms, 31.3MB)
테스트 7 〉	통과 (0.16ms, 31.4MB)
테스트 8 〉	통과 (0.17ms, 31MB)
테스트 9 〉	통과 (0.15ms, 31.1MB)
테스트 10 〉	통과 (0.16ms, 31.4MB)
테스트 11 〉	통과 (0.15ms, 31.3MB)
테스트 12 〉	통과 (0.15ms, 31.1MB)
테스트 13 〉	통과 (0.15ms, 31.1MB)
테스트 14 〉	통과 (0.15ms, 31.2MB)
테스트 15 〉	통과 (0.17ms, 31.1MB)
테스트 16 〉	통과 (0.16ms, 31.4MB)
테스트 17 〉	통과 (0.18ms, 31.2MB)
테스트 18 〉	통과 (0.15ms, 31.2MB)
테스트 19 〉	통과 (0.17ms, 31.3MB)
테스트 20 〉	통과 (0.29ms, 31.3MB)
테스트 21 〉	통과 (0.15ms, 31MB)
테스트 22 〉	통과 (0.25ms, 31.3MB)
테스트 23 〉	통과 (0.16ms, 31.5MB)
```