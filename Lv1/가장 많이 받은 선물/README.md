# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/258712">가장 많이 받은 선물</a>

### 문제설명

선물을 직접 전하기 힘들 때 카카오톡 선물하기 기능을 이용해 축하 선물을 보낼 수 있습니다. 당신의 친구들이 이번 달까지 선물을 주고받은 기록을 바탕으로 다음 달에 누가 선물을 많이 받을지 예측하려고 합니다.

 - 두 사람이 선물을 주고받은 기록이 있다면, 이번 달까지 두 사람 사이에 더 많은 선물을 준 사람이 다음 달에 선물을 하나 받습니다.
   - 예를 들어 A가 B에게 선물을 5번 줬고, B가 A에게 선물을 3번 줬다면 다음 달엔 A가 B에게 선물을 하나 받습니다.
 - 두 사람이 선물을 주고받은 기록이 하나도 없거나 주고받은 수가 같다면, 선물 지수가 더 큰 사람이 선물 지수가 더 작은 사람에게 선물을 하나 받습니다.
   - 선물 지수는 이번 달까지 자신이 친구들에게 준 선물의 수에서 받은 선물의 수를 뺀 값입니다.
   - 예를 들어 A가 친구들에게 준 선물이 3개고 받은 선물이 10개라면 A의 선물 지수는 -7입니다. B가 친구들에게 준 선물이 3개고 받은 선물이 2개라면 B의 선물 지수는 1입니다. 만약 A와 B가 선물을 주고받은 적이 없거나 정확히 같은 수로 선물을 주고받았다면, 다음 달엔 B가 A에게 선물을 하나 받습니다.
   - 만약 두 사람의 선물 지수도 같다면 다음 달에 선물을 주고받지 않습니다.

위에서 설명한 규칙대로 다음 달에 선물을 주고받을 때, 당신은 선물을 가장 많이 받을 친구가 받을 선물의 수를 알고 싶습니다.

친구들의 이름을 담은 1차원 문자열 배열 friends 이번 달까지 친구들이 주고받은 선물 기록을 담은 1차원 문자열 배열 gifts가 매개변수로 주어집니다. 이때, 다음달에 가장 많은 선물을 받는 친구가 받을 선물의 수를 return 하도록 solution 함수를 완성해 주세요.

***

### 제한사항

 - 2 ≤ friends의 길이 = 친구들의 수 ≤ 50
   - friends의 원소는 친구의 이름을 의미하는 알파벳 소문자로 이루어진 길이가 10 이하인 문자열입니다.
   - 이름이 같은 친구는 없습니다.
 - 1 ≤ gifts의 길이 ≤ 10,000
   - gifts의 원소는 "A B"형태의 문자열입니다. A는 선물을 준 친구의 이름을 B는 선물을 받은 친구의 이름을 의미하며 공백 하나로 구분됩니다.
   - A와 B는 friends의 원소이며 A와 B가 같은 이름인 경우는 존재하지 않습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(string[] friends, string[] gifts) {
        int answer = 0;
        Dictionary<string, Dictionary<string, int>> giftCounts = new Dictionary<string, Dictionary<string, int>>();
        Dictionary<string, int> totalCounts = new Dictionary<string, int>();
        Dictionary<string, int> answerCounts = new Dictionary<string, int>();
        
        for(int i = 0; i < friends.Length; i++) {
            for(int j = 0; j < friends.Length; j++) {
                if(i == j) {
                    continue;
                }
                if(!giftCounts.ContainsKey(friends[i])) {
                    giftCounts[friends[i]] = new Dictionary<string, int>();
                }
                giftCounts[friends[i]][friends[j]] = 0;
            }
            totalCounts[friends[i]] = 0;
            answerCounts[friends[i]] = 0;
        }
        
        for(int i = 0; i < gifts.Length; i++) {
            string[] str = gifts[i].Split(" ");
            giftCounts[str[0]][str[1]]++;
            totalCounts[str[0]]++;
            totalCounts[str[1]]--;
        }
        
        for(int i = 0; i < friends.Length; i++) {
            for(int j = 0; j < friends.Length; j++) {
                if(i == j) {
                    continue;
                }
                if(giftCounts[friends[i]][friends[j]] == giftCounts[friends[j]][friends[i]]) {
                    if(totalCounts[friends[i]] > totalCounts[friends[j]]) {
                        answerCounts[friends[i]]++;
                    }
                }else if(giftCounts[friends[i]][friends[j]] > giftCounts[friends[j]][friends[i]]) {
                    answerCounts[friends[i]]++;
                }
            }
        }
        
        foreach(int count in answerCounts.Values) {
            answer = Math.Max(answer,count);
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.65ms, 30.9MB)
테스트 2 〉	통과 (2.74ms, 31.2MB)
테스트 3 〉	통과 (2.71ms, 30.9MB)
테스트 4 〉	통과 (2.78ms, 31.4MB)
테스트 5 〉	통과 (3.80ms, 31.5MB)
테스트 6 〉	통과 (2.92ms, 31.4MB)
테스트 7 〉	통과 (3.62ms, 31.4MB)
테스트 8 〉	통과 (3.56ms, 31.6MB)
테스트 9 〉	통과 (6.57ms, 32.4MB)
테스트 10 〉	통과 (6.85ms, 32.7MB)
테스트 11 〉	통과 (6.26ms, 32.2MB)
테스트 12 〉	통과 (5.54ms, 32.1MB)
테스트 13 〉	통과 (10.16ms, 33.9MB)
테스트 14 〉	통과 (9.32ms, 33.7MB)
테스트 15 〉	통과 (10.10ms, 33.5MB)
테스트 16 〉	통과 (11.47ms, 34.1MB)
테스트 17 〉	통과 (2.81ms, 31.1MB
```