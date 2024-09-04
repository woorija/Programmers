# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49994">방문 길이</a>

### 문제설명

게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

 - U: 위쪽으로 한 칸 가기
 - D: 아래쪽으로 한 칸 가기
 - R: 오른쪽으로 한 칸 가기
 - L: 왼쪽으로 한 칸 가기

캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.

이때, 우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어  "ULURRDLLU"로 명령했다면 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)

단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.

명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.

***

### 제한사항

 - dirs는 string형으로 주어지며, 'U', 'D', 'R', 'L' 이외에 문자는 주어지지 않습니다.
 - dirs의 길이는 500 이하의 자연수입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    HashSet<(int, int, int, int)> hashSet;
    public int solution(string dirs) {
        int curX = 0;
        int curY = 0;
        int nextX = 0;
        int nextY = 0;
        hashSet = new HashSet<(int, int, int, int)>();
        for(int i = 0; i < dirs.Length; i++) {
            switch(dirs[i]) {
                case 'U':
                    nextY = Math.Min(nextY + 1, 5);
                    Set(curX, curY, nextX, nextY);
                    curY = nextY;
                    break;
                case 'D':
                    nextY = Math.Max(nextY - 1, -5);
                    Set(curX, curY, nextX, nextY);
                    curY = nextY;
                    break;
                case 'R':
                    nextX = Math.Min(nextX + 1, 5);
                    Set(curX, curY, nextX, nextY);
                    curX = nextX;
                    break;
                case 'L':
                    nextX = Math.Max(nextX - 1, -5);
                    Set(curX, curY, nextX, nextY);
                    curX = nextX;
                    break;
            }
        }
        return hashSet.Count;
    }
    void Set(int curX, int curY, int nextX, int nextY){
        if(curX == nextX && curY == nextY) return;
        if(curY == nextY) {
            if(curX < nextX) {
                hashSet.Add((curX, nextX, curY, nextY));
            }else{
                hashSet.Add((nextX, curX, curY, nextY));
            }
        }else{
            if(curY < nextY) {
                hashSet.Add((nextX, curX, curY, nextY));
            }else{
                hashSet.Add((nextX, curX, nextY, curY));
            }
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.21ms, 31.1MB)
테스트 2 〉	통과 (1.96ms, 31.1MB)
테스트 3 〉	통과 (1.96ms, 31.1MB)
테스트 4 〉	통과 (2.28ms, 31.3MB)
테스트 5 〉	통과 (2.33ms, 31.2MB)
테스트 6 〉	통과 (2.43ms, 31.3MB)
테스트 7 〉	통과 (2.00ms, 31.1MB)
테스트 8 〉	통과 (2.25ms, 31.4MB)
테스트 9 〉	통과 (2.85ms, 31.4MB)
테스트 10 〉	통과 (2.34ms, 31.4MB)
테스트 11 〉	통과 (3.68ms, 31.3MB)
테스트 12 〉	통과 (3.52ms, 31.5MB)
테스트 13 〉	통과 (2.38ms, 31.2MB)
테스트 14 〉	통과 (2.71ms, 31.5MB)
테스트 15 〉	통과 (2.57ms, 31.7MB)
테스트 16 〉	통과 (2.58ms, 31.3MB)
테스트 17 〉	통과 (2.31ms, 31.4MB)
테스트 18 〉	통과 (2.46ms, 31.3MB)
테스트 19 〉	통과 (2.59ms, 31.2MB)
```