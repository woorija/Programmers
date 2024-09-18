# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12946">하노이의 탑</a>

### 문제설명

하노이 탑(Tower of Hanoi)은 퍼즐의 일종입니다. 세 개의 기둥과 이 기동에 꽂을 수 있는 크기가 다양한 원판들이 있고, 퍼즐을 시작하기 전에는 한 기둥에 원판들이 작은 것이 위에 있도록 순서대로 쌓여 있습니다. 게임의 목적은 다음 두 가지 조건을 만족시키면서, 한 기둥에 꽂힌 원판들을 그 순서 그대로 다른 기둥으로 옮겨서 다시 쌓는 것입니다.

 1. 한 번에 하나의 원판만 옮길 수 있습니다.
 2. 큰 원판이 작은 원판 위에 있어서는 안됩니다.

하노이 탑의 세 개의 기둥을 왼쪽 부터 1번, 2번, 3번이라고 하겠습니다. 1번에는 n개의 원판이 있고 이 n개의 원판을 3번 원판으로 최소 횟수로 옮기려고 합니다.

1번 기둥에 있는 원판의 개수 n이 매개변수로 주어질 때, n개의 원판을 3번 원판으로 최소로 옮기는 방법을 return하는 solution를 완성해주세요.

***

### 제한사항

 - n은 15이하의 자연수 입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int index = 0;
    int[,] answer;
    public int[,] solution(int n) {
        answer = new int[(int)Math.Pow(2, n) - 1,2];
        Hanoi(n, 1, 2, 3);
        return answer;
    }
    void Hanoi(int _num, int _start, int _middle, int _end) {
        if(_num == 0) return;
        Hanoi(_num - 1, _start, _end, _middle);
        answer[index,0] = _start;
        answer[index,1] = _end;
        index++;
        Hanoi(_num - 1, _middle, _start, _end);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.43ms, 31.5MB)
테스트 2 〉	통과 (0.55ms, 31.5MB)
테스트 3 〉	통과 (0.54ms, 31.3MB)
테스트 4 〉	통과 (0.38ms, 31.7MB)
테스트 5 〉	통과 (0.52ms, 31.4MB)
테스트 6 〉	통과 (0.57ms, 31.4MB)
테스트 7 〉	통과 (0.41ms, 31.6MB)
테스트 8 〉	통과 (0.43ms, 31.5MB)
테스트 9 〉	통과 (0.56ms, 31.9MB)
테스트 10 〉	통과 (0.44ms, 32.1MB)
테스트 11 〉	통과 (0.76ms, 32.8MB)
테스트 12 〉	통과 (0.66ms, 34.1MB)
테스트 13 〉	통과 (0.84ms, 38.9MB)
```