# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/159993">미로 탈출</a>

### 문제설명

1 x 1 크기의 칸들로 이루어진 직사각형 격자 형태의 미로에서 탈출하려고 합니다. 각 칸은 통로 또는 벽으로 구성되어 있으며, 벽으로 된 칸은 지나갈 수 없고 통로로 된 칸으로만 이동할 수 있습니다. 통로들 중 한 칸에는 미로를 빠져나가는 문이 있는데, 이 문은 레버를 당겨서만 열 수 있습니다. 레버 또한 통로들 중 한 칸에 있습니다. 따라서, 출발 지점에서 먼저 레버가 있는 칸으로 이동하여 레버를 당긴 후 미로를 빠져나가는 문이 있는 칸으로 이동하면 됩니다. 이때 아직 레버를 당기지 않았더라도 출구가 있는 칸을 지나갈 수 있습니다. 미로에서 한 칸을 이동하는데 1초가 걸린다고 할 때, 최대한 빠르게 미로를 빠져나가는데 걸리는 시간을 구하려 합니다.

미로를 나타낸 문자열 배열 maps가 매개변수로 주어질 때, 미로를 탈출하는데 필요한 최소 시간을 return 하는 solution 함수를 완성해주세요. 만약, 탈출할 수 없다면 -1을 return 해주세요.

***

### 제한사항

 - 5 ≤ maps의 길이 ≤ 100
   - 5 ≤ maps[i]의 길이 ≤ 100
   - maps[i]는 다음 5개의 문자들로만 이루어져 있습니다.
     - S : 시작 지점
     - E : 출구
     - L : 레버
     - O : 통로
     - X : 벽
   - 시작 지점과 출구, 레버는 항상 다른 곳에 존재하며 한 개씩만 존재합니다.
   - 출구는 레버가 당겨지지 않아도 지나갈 수 있으며, 모든 통로, 출구, 레버, 시작점은 여러 번 지나갈 수 있습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Counter {
    public int indexX;
    public int indexY;
    public int count;
    public Counter(int _indexX, int _indexY, int _count){
        indexX = _indexX;
        indexY = _indexY;
        count = _count;
    }
}
public class Solution {
    HashSet<(int,int)> moveTo;
    Queue<Counter> queue;
    int indexX;
    int indexY;
    int lengthX;
    int lengthY;
    public int solution(string[] maps) {
        moveTo = new HashSet<(int,int)>();
        queue = new Queue<Counter>();
        int answer = 0;
        lengthY = maps.Length;
        lengthX = maps[0].Length;
        int countS = 0;
        int countE = 0;
        int indexXS = 0;
        int indexYS = 0;
        int indexXE = 0;
        int indexYE = 0;
        
        for(int i = 0; i < lengthY; i++) {
            if(maps[i].IndexOf('L') != -1) {
                indexY = i;
                indexX = maps[i].IndexOf('L');
            }
            if(maps[i].IndexOf('E') != -1) {
                indexYE = i;
                indexXE = maps[i].IndexOf('E');
            }
            if(maps[i].IndexOf('S') != -1) {
                indexYS = i;
                indexXS = maps[i].IndexOf('S');
            }
        }
        Enqueue(maps, indexX, indexY, 0);
        while(queue.Count != 0) {
            Counter counter = queue.Dequeue();
            int tempX = counter.indexX;
            int tempY = counter.indexY;
            int count = counter.count;
            if(tempX == indexXS && tempY == indexYS) {
                countS = count;
            }
            if(tempX == indexXE && tempY == indexYE) {
                countE = count;
            }
            if(countS != 0 && countE != 0){
                break;
            }
            Enqueue(maps, tempX - 1, tempY, count + 1);
            Enqueue(maps, tempX + 1, tempY, count + 1);
            Enqueue(maps, tempX, tempY - 1, count + 1);
            Enqueue(maps, tempX, tempY + 1, count + 1);
        }
        if(countS == 0 || countE == 0){
            return -1;
        }
        return countS + countE;
    }
    public void Enqueue(string[] _maps, int _indexX, int _indexY, int _count) {
        if(moveTo.Contains((_indexX,_indexY))) return;
        moveTo.Add((_indexX,_indexY));
        if(_indexX < 0 || _indexY < 0 || _indexX == lengthX || _indexY == lengthY) return;
        if(_maps[_indexY][_indexX].Equals('X')) return;
        queue.Enqueue(new Counter(_indexX, _indexY, _count));
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.28ms, 31.3MB)
테스트 2 〉	통과 (2.91ms, 31.3MB)
테스트 3 〉	통과 (2.92ms, 31.1MB)
테스트 4 〉	통과 (2.75ms, 31.1MB)
테스트 5 〉	통과 (2.97ms, 31.3MB)
테스트 6 〉	통과 (2.75ms, 31MB)
테스트 7 〉	통과 (2.96ms, 31.5MB)
테스트 8 〉	통과 (3.12ms, 31.5MB)
테스트 9 〉	통과 (2.71ms, 31.6MB)
테스트 10 〉	통과 (4.06ms, 31.4MB)
테스트 11 〉	통과 (3.13ms, 31.4MB)
테스트 12 〉	통과 (3.52ms, 31.4MB)
테스트 13 〉	통과 (3.38ms, 31.5MB)
테스트 14 〉	통과 (3.43ms, 31.7MB)
테스트 15 〉	통과 (3.37ms, 31.5MB)
테스트 16 〉	통과 (4.73ms, 31.7MB)
테스트 17 〉	통과 (4.72ms, 31.3MB)
테스트 18 〉	통과 (2.72ms, 31.3MB)
테스트 19 〉	통과 (2.75ms, 31.3MB)
테스트 20 〉	통과 (4.44ms, 31.7MB)
테스트 21 〉	통과 (3.26ms, 31.5MB)
테스트 22 〉	통과 (3.08ms, 31.1MB)
테스트 23 〉	통과 (2.73ms, 31.3MB)
```