# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/1844">게임 맵 최단거리</a>

### 문제설명

ROR 게임은 두 팀으로 나누어서 진행하며, 상대 팀 진영을 먼저 파괴하면 이기는 게임입니다. 따라서, 각 팀은 상대 팀 진영에 최대한 빨리 도착하는 것이 유리합니다.

지금부터 당신은 한 팀의 팀원이 되어 게임을 진행하려고 합니다. 다음은 5 x 5 크기의 맵에, 당신의 캐릭터가 (행: 1, 열: 1) 위치에 있고, 상대 팀 진영은 (행: 5, 열: 5) 위치에 있는 경우의 예시입니다.

□ ■ □ □ □

□ ■ □ ■ □

□ ■ □ □ □

□ □ □ ■ □

■ ■ ■ ■ □

위 그림에서 검은색 부분은 벽으로 막혀있어 갈 수 없는 길이며, 흰색 부분은 갈 수 있는 길입니다. 캐릭터가 움직일 때는 동, 서, 남, 북 방향으로 한 칸씩 이동하며, 게임 맵을 벗어난 길은 갈 수 없습니다.

만약, 상대 팀이 자신의 팀 진영 주위에 벽을 세워두었다면 상대 팀 진영에 도착하지 못할 수도 있습니다. 예를 들어, 다음과 같은 경우에 당신의 캐릭터는 상대 팀 진영에 도착할 수 없습니다.

□ ■ □ □ □

□ ■ □ ■ □

□ ■ □ □ □

□ □ □ ■ ■

■ ■ ■ ■ □

게임 맵의 상태 maps가 매개변수로 주어질 때, 캐릭터가 상대 팀 진영에 도착하기 위해서 지나가야 하는 칸의 개수의 최솟값을 return 하도록 solution 함수를 완성해주세요. 단, 상대 팀 진영에 도착할 수 없을 때는 -1을 return 해주세요.

***

### 제한사항

 - maps는 n x m 크기의 게임 맵의 상태가 들어있는 2차원 배열로, n과 m은 각각 1 이상 100 이하의 자연수입니다.
   - n과 m은 서로 같을 수도, 다를 수도 있지만, n과 m이 모두 1인 경우는 입력으로 주어지지 않습니다.
 - maps는 0과 1로만 이루어져 있으며, 0은 벽이 있는 자리, 1은 벽이 없는 자리를 나타냅니다.
 - 처음에 캐릭터는 게임 맵의 좌측 상단인 (1, 1) 위치에 있으며, 상대방 진영은 게임 맵의 우측 하단인 (n, m) 위치에 있습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Counter{
    public int x;
    public int y;
    public int count;
    public Counter(int _x, int _y, int _count){
        x = _x;
        y = _y;
        count = _count;
    }
}
class Solution {
    Queue<Counter> queue = new Queue<Counter>();
    int row;
    int col;
    public int solution(int[,] maps) {
        int answer = 0;
        row = maps.GetLength(0);
        col = maps.GetLength(1);
        Counter counter = new Counter(0,0,1);
        queue.Enqueue(counter);
        while(queue.Count != 0){
            counter = queue.Dequeue();
            int x = counter.x;
            int y = counter.y;
            int count = counter.count;
            
            if(maps[x,y] != 1) continue;
            
            maps[x,y] = count;
            Enqueue(new Counter(x - 1, y, count + 1), maps);
            Enqueue(new Counter(x + 1, y, count + 1), maps);
            Enqueue(new Counter(x, y + 1, count + 1), maps);
            Enqueue(new Counter(x, y - 1, count + 1), maps);
            if(maps[row - 1, col - 1] != 1) break;
        }
        answer = maps[row - 1,col - 1] == 1 ? -1 : maps[row - 1,col - 1];
        return answer;
    }
    void Enqueue(Counter counter, int[,] maps){
        int x = counter.x;
        int y = counter.y;
        if(x < 0 || y < 0 || x > row - 1 || y > col - 1) return;
        if(maps[x,y] != 1) return;
        queue.Enqueue(counter);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.61ms, 31.5MB)
테스트 2 〉	통과 (0.60ms, 31.5MB)
테스트 3 〉	통과 (0.63ms, 31.4MB)
테스트 4 〉	통과 (0.63ms, 31.2MB)
테스트 5 〉	통과 (0.61ms, 31.3MB)
테스트 6 〉	통과 (0.62ms, 31.5MB)
테스트 7 〉	통과 (0.62ms, 31.2MB)
테스트 8 〉	통과 (0.61ms, 31.3MB)
테스트 9 〉	통과 (0.61ms, 31.3MB)
테스트 10 〉	통과 (0.62ms, 31.4MB)
테스트 11 〉	통과 (0.63ms, 31.4MB)
테스트 12 〉	통과 (0.66ms, 31.1MB)
테스트 13 〉	통과 (0.64ms, 31.2MB)
테스트 14 〉	통과 (0.62ms, 31.3MB)
테스트 15 〉	통과 (0.62ms, 31.4MB)
테스트 16 〉	통과 (0.61ms, 31.2MB)
테스트 17 〉	통과 (0.60ms, 31.2MB)
테스트 18 〉	통과 (0.60ms, 31.5MB)
테스트 19 〉	통과 (0.60ms, 31.3MB)
테스트 20 〉	통과 (0.59ms, 31.5MB)
테스트 21 〉	통과 (0.60ms, 31.3MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (2.08ms, 32.8MB)
테스트 2 〉	통과 (1.02ms, 32MB)
테스트 3 〉	통과 (1.68ms, 32.4MB)
테스트 4 〉	통과 (1.31ms, 32MB)
```