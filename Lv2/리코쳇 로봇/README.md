# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/169199">리코쳇 로봇</a>

### 문제설명

리코쳇 로봇이라는 보드게임이 있습니다.

이 보드게임은 격자모양 게임판 위에서 말을 움직이는 게임으로, 시작 위치에서 출발한 뒤 목표 위치에 정확하게 멈추기 위해 최소 몇 번의 이동이 필요한지 말하는 게임입니다.

이 게임에서 말의 이동은 현재 위치에서 상, 하, 좌, 우 중 한 방향으로 게임판 위의 장애물이나 게임판 가장자리까지 부딪힐 때까지 미끄러져 움직이는 것을 한 번의 이동으로 정의합니다.

다음은 보드게임판을 나타낸 예시입니다. ("."은 빈 공간을, "R"은 로봇의 처음 위치를, "D"는 장애물의 위치를, "G"는 목표지점을 나타냅니다.)

```
...D..R
.D.G...
....D.D
D....D.
..D....
```

이때 최소 움직임은 7번이며 "R" 위치에서 아래, 왼쪽, 위, 왼쪽, 아래, 오른쪽, 위 순서로 움직이면 "G" 위치에 멈춰 설 수 있습니다.

게임판의 상태를 나타내는 문자열 배열 board가 주어졌을 때, 말이 목표위치에 도달하는데 최소 몇 번 이동해야 하는지 return 하는 solution함수를 완성해주세요. 만약 목표위치에 도달할 수 없다면 -1을 return 해주세요.

***

### 제한사항

 - 3 ≤ board의 길이 ≤ 100
   - 3 ≤ board의 원소의 길이 ≤ 100
   - board의 원소의 길이는 모두 동일합니다.
   - 문자열은 ".", "D", "R", "G"로만 구성되어 있으며 각각 빈 공간, 장애물, 로봇의 처음 위치, 목표 지점을 나타냅니다.
   - "R"과 "G"는 한 번씩 등장합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public struct Data {
    public int x;
    public int y;
    public int count;
    public Data(int _x, int _y, int _count) {
        x = _x;
        y = _y;
        count = _count;
    }
}

public class Solution {
    int row;
    int col;
    int[,] map;
    Queue<Data> queue;
    HashSet<(int,int)> used;
    public int solution(string[] board) {
        int answer = 0;
        row = board[0].Length;
        col = board.Length;
        map = new int[row,col];
        queue = new Queue<Data>();
        used = new HashSet<(int,int)>();
        int answerX = 0;
        int answerY = 0;
        
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                map[i,j] = int.MaxValue;
                if(board[j][i] == 'R') {
                    Enqueue(i, j, 0);
                }
                if(board[j][i] == 'G') {
                    answerX = i;
                    answerY = j;
                }
            }
        }
        
        while(queue.Count != 0) {
            Data current = queue.Dequeue();
            int x = current.x;
            int y = current.y;
            int count = current.count;
            if(map[x,y] != int.MaxValue) {
                break;
            }
            
            map[x,y] = count;
            count++;
            
            for(int i = 0; i < col; i++) {
                y++;
                if(y == col || board[y][x] == 'D') {
                    y--;
                    Enqueue(x, y, count);
                }
            }
            x = current.x;
            y = current.y;
            for(int i = 0; i < col; i++) {
                y--;
                if(y == -1 || board[y][x] == 'D') {
                    y++;
                    Enqueue(x, y, count);
                }
            }
            x = current.x;
            y = current.y;
            for(int i = 0; i < row; i++) {
                x++;
                if(x == row || board[y][x] == 'D') {
                    x--;
                    Enqueue(x, y, count);
                }
            }
            x = current.x;
            y = current.y;
            for(int i = 0; i < row; i++) {
                x--;
                if(x == -1 || board[y][x] == 'D') {
                    x++;
                    Enqueue(x, y, count);
                }
            }
        }
        
        return map[answerX,answerY] == int.MaxValue ? -1 : map[answerX,answerY];
    }
    
    void Enqueue(int _x, int _y, int _count) {
        if(used.Contains((_x,_y))) return;
        queue.Enqueue(new Data(_x, _y, _count));
        used.Add((_x,_y));
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (27.28ms, 31.2MB)
테스트 2 〉	통과 (42.06ms, 31.4MB)
테스트 3 〉	통과 (5.39ms, 30.9MB)
테스트 4 〉	통과 (7.32ms, 31.1MB)
테스트 5 〉	통과 (6.44ms, 31.2MB)
테스트 6 〉	통과 (5.84ms, 31.2MB)
테스트 7 〉	통과 (41.59ms, 31.4MB)
테스트 8 〉	통과 (7.66ms, 31.3MB)
테스트 9 〉	통과 (9.86ms, 31.4MB)
테스트 10 〉	통과 (14.94ms, 31.2MB)
테스트 11 〉	통과 (3.34ms, 31.1MB)
테스트 12 〉	통과 (4.07ms, 31.1MB)
테스트 13 〉	통과 (4.17ms, 30.8MB)
테스트 14 〉	통과 (12.92ms, 31.3MB)
테스트 15 〉	통과 (4.80ms, 31.4MB)
테스트 16 〉	통과 (16.42ms, 31MB)
테스트 17 〉	통과 (9.05ms, 31.1MB)
테스트 18 〉	통과 (7.23ms, 31.2MB)
테스트 19 〉	통과 (8.04ms, 31.2MB)
테스트 20 〉	통과 (3.52ms, 31.2MB)
테스트 21 〉	통과 (19.61ms, 31.4MB)
테스트 22 〉	통과 (4.66ms, 31.1MB)
테스트 23 〉	통과 (4.26ms, 31.3MB)
테스트 24 〉	통과 (25.98ms, 31.1MB)
테스트 25 〉	통과 (14.14ms, 31.3MB)
테스트 26 〉	통과 (9.05ms, 31.3MB)
테스트 27 〉	통과 (4.54ms, 31.3MB)
```