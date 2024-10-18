# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42840">모의고사</a>

### 문제설명

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 시험은 최대 10,000 문제로 구성되어있습니다.
 - 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
 - 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int[] answers) {
        List<int> answer = new List<int>();
        int[] answer1 = new int[]{ 1, 2, 3, 4, 5 };
        int[] answer2 = new int[]{ 2, 1, 2, 3, 2, 4, 2, 5 };
        int[] answer3 = new int[]{ 3, 3, 1, 1, 2, 2, 4, 4, 5, 5 };
        
        int[] answerCounts = new int[3];
        int max = 0;
        for(int i = 0; i < answers.Length; i++) {
            if(answers[i] == answer1[i % answer1.Length]) {
                answerCounts[0]++;
            }
            if(answers[i] == answer2[i % answer2.Length]) {
                answerCounts[1]++;
            }
            if(answers[i] == answer3[i % answer3.Length]) {
                answerCounts[2]++;
            }
        }
        max = Math.Max(answerCounts[0], Math.Max(answerCounts[1], answerCounts[2]));
        for(int i = 0; i < answerCounts.Length; i++) {
            if(answerCounts[i] == max) {
                answer.Add(i + 1);
            }
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.95ms, 31.3MB)
테스트 2 〉	통과 (0.93ms, 30.8MB)
테스트 3 〉	통과 (0.69ms, 31.3MB)
테스트 4 〉	통과 (1.03ms, 31MB)
테스트 5 〉	통과 (0.97ms, 31.1MB)
테스트 6 〉	통과 (0.65ms, 31.1MB)
테스트 7 〉	통과 (0.75ms, 31.3MB)
테스트 8 〉	통과 (0.88ms, 31.3MB)
테스트 9 〉	통과 (0.83ms, 31.2MB)
테스트 10 〉	통과 (0.72ms, 31.3MB)
테스트 11 〉	통과 (1.15ms, 31MB)
테스트 12 〉	통과 (0.79ms, 30.9MB)
테스트 13 〉	통과 (0.69ms, 31.3MB)
테스트 14 〉	통과 (0.72ms, 31MB)
```