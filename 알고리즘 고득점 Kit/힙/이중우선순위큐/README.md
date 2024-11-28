# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42628">이중우선순위큐</a>

### 문제설명

이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

| 명령어 | 수신 탑(높이) |
| ------- | ------- |
| I 숫자 | 큐에 주어진 숫자를 삽입합니다. |
| D 1 | 큐에서 최댓값을 삭제합니다. |
| D -1 | 큐에서 최솟값을 삭제합니다. |

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

***

### 제한사항

 - operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
 - operations의 원소는 큐가 수행할 연산을 나타냅니다.
   - 원소는 “명령어 데이터” 형식으로 주어집니다.
   - 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
 - 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(string[] operations) {
        int[] answer = new int[2];
        List<int> list = new List<int>();
        for(int i = 0; i < operations.Length; i++) {
            string[] oper = operations[i].Split(" ");
            string key = oper[0];
            int num = int.Parse(oper[1]);
            if(key.Equals("I")) {
                list.Add(num);
            }else{
                if(list.Count == 0) {
                    continue;
                }
                if(num == 1) {
                    list.RemoveAt(list.Count - 1);
                }else{
                    list.RemoveAt(0);
                }
            }
            list.Sort();
        }
        if(list.Count != 0) {
        answer[0] = list[list.Count - 1];
        answer[1] = list[0];
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.56ms, 31.8MB)
테스트 2 〉	통과 (2.47ms, 31.3MB)
테스트 3 〉	통과 (2.49ms, 31.5MB)
테스트 4 〉	통과 (0.92ms, 31.4MB)
테스트 5 〉	통과 (3.16ms, 31.7MB)
테스트 6 〉	통과 (3.16ms, 31.4MB)
테스트 7 〉	통과 (1974.25ms, 47.6MB)
테스트 8 〉	통과 (2.43ms, 31.7MB)
테스트 9 〉	통과 (3.63ms, 31.6MB)
```