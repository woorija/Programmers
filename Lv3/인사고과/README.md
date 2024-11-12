# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/152995">인사고과</a>

### 문제설명

완호네 회사는 연말마다 1년 간의 인사고과에 따라 인센티브를 지급합니다. 각 사원마다 근무 태도 점수와 동료 평가 점수가 기록되어 있는데 만약 어떤 사원이 다른 임의의 사원보다 두 점수가 모두 낮은 경우가 한 번이라도 있다면 그 사원은 인센티브를 받지 못합니다. 그렇지 않은 사원들에 대해서는 두 점수의 합이 높은 순으로 석차를 내어 석차에 따라 인센티브가 차등 지급됩니다. 이때, 두 점수의 합이 동일한 사원들은 동석차이며, 동석차의 수만큼 다음 석차는 건너 뜁니다. 예를 들어 점수의 합이 가장 큰 사원이 2명이라면 1등이 2명이고 2등 없이 다음 석차는 3등부터입니다.

각 사원의 근무 태도 점수와 동료 평가 점수 목록 scores이 주어졌을 때, 완호의 석차를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ scores의 길이 ≤ 100,000
 - scores의 각 행은 한 사원의 근무 태도 점수와 동료 평가 점수를 나타내며 [a, b] 형태입니다.
   - scores[0]은 완호의 점수입니다.
   - 0 ≤ a, b ≤ 100,000
 - 완호가 인센티브를 받지 못하는 경우 -1을 return 합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Score : IComparable<Score> {
    public int scoreA;
    public int scoreB;
    
    public Score(int _a, int _b) {
        scoreA = _a;
        scoreB = _b;
    }
    
    int IComparable<Score>.CompareTo(Score _other) {
        int sum = scoreA + scoreB;
        int otherSum = _other.scoreA + _other.scoreB;
        
        return otherSum.CompareTo(sum);
    }
    
    public int sum => scoreA+scoreB;
}

public class Solution {
    List<Score> list;
    public int solution(int[,] scores) {
        int answer = 1;
        int score = scores[0,0] + scores[0,1];
        list = new List<Score>();
        
        list.Add(new Score(scores[0,0], scores[0,1]));
        
        for(int i = 1; i < scores.GetLength(0); i++) {
            if(scores[0,0] < scores[i,0] && scores[0,1] < scores[i,1]) {
                return -1;
            }
            
            if(score <= scores[i,0] + scores[i,1]) {
                list.Add(new Score(scores[i,0], scores[i,1]));
            }
        }
        
        list.Sort();
        
        for(int i = 0; i < list.Count; i++) {
            if(list[i].sum == score) {
                break;
            }
            if(Check(list[i])) {
                answer++;
            }
        }
        
        return answer;
    }
    
    bool Check(Score _score) {
        bool flag = true;
        for(int i = 0; i < list.Count; i++) {
            if(_score.sum + 1 == list[i].sum) {
                break;
            }
            if(_score.scoreA < list[i].scoreA && _score.scoreB < list[i].scoreB) {
                flag = false;
                break;
            }
        }
        return flag;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.85ms, 31.5MB)
테스트 2 〉	통과 (1.74ms, 31.5MB)
테스트 3 〉	통과 (1.71ms, 31.6MB)
테스트 4 〉	통과 (1.69ms, 31.2MB)
테스트 5 〉	통과 (0.85ms, 31.6MB)
테스트 6 〉	통과 (0.77ms, 31.5MB)
테스트 7 〉	통과 (0.85ms, 31.2MB)
테스트 8 〉	통과 (2.40ms, 31MB)
테스트 9 〉	통과 (0.80ms, 31.2MB)
테스트 10 〉	통과 (1.81ms, 31.6MB)
테스트 11 〉	통과 (1.87ms, 30.9MB)
테스트 12 〉	통과 (0.92ms, 31.4MB)
테스트 13 〉	통과 (0.78ms, 31.6MB)
테스트 14 〉	통과 (1.69ms, 31.5MB)
테스트 15 〉	통과 (0.79ms, 31.7MB)
테스트 16 〉	통과 (1.98ms, 31.6MB)
테스트 17 〉	통과 (1.69ms, 32.1MB)
테스트 18 〉	통과 (0.90ms, 32MB)
테스트 19 〉	통과 (0.84ms, 35.4MB)
테스트 20 〉	통과 (0.89ms, 35.6MB)
테스트 21 〉	통과 (30.24ms, 47.1MB)
테스트 22 〉	통과 (12.67ms, 42MB)
테스트 23 〉	통과 (2.11ms, 41.8MB)
테스트 24 〉	통과 (6017.90ms, 42MB)
테스트 25 〉	통과 (1288.74ms, 41.9MB)
테스트 26 〉	통과 (1.60ms, 31.4MB)
테스트 27 〉	통과 (1.64ms, 31MB)
테스트 28 〉	통과 (1.57ms, 31.1MB)
```