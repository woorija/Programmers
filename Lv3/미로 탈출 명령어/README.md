# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/150365">미로 탈출 명령어</a>

### 문제설명

n x m 격자 미로가 주어집니다. 당신은 미로의 (x, y)에서 출발해 (r, c)로 이동해서 탈출해야 합니다.

단, 미로를 탈출하는 조건이 세 가지 있습니다.

 1. 격자의 바깥으로는 나갈 수 없습니다.
 2. (x, y)에서 (r, c)까지 이동하는 거리가 총 k여야 합니다. 이때, (x, y)와 (r, c)격자를 포함해, 같은 격자를 두 번 이상 방문해도 됩니다.
 3. 미로에서 탈출한 경로를 문자열로 나타냈을 때, 문자열이 사전 순으로 가장 빠른 경로로 탈출해야 합니다.

이동 경로는 다음과 같이 문자열로 바꿀 수 있습니다.

 - l: 왼쪽으로 한 칸 이동
 - r: 오른쪽으로 한 칸 이동
 - u: 위쪽으로 한 칸 이동
 - d: 아래쪽으로 한 칸 이동

예를 들어, 왼쪽으로 한 칸, 위로 한 칸, 왼쪽으로 한 칸 움직였다면, 문자열 "lul"로 나타낼 수 있습니다.

미로에서는 인접한 상, 하, 좌, 우 격자로 한 칸씩 이동할 수 있습니다.

예를 들어 다음과 같이 3 x 4 격자가 있다고 가정해 보겠습니다.

```
....
..S.
E...
```

미로의 좌측 상단은 (1, 1)이고 우측 하단은 (3, 4)입니다. .은 빈 공간, S는 출발 지점, E는 탈출 지점입니다.

탈출까지 이동해야 하는 거리 k가 5라면 다음과 같은 경로로 탈출할 수 있습니다.

 1. lldud
 2. ulldd
 3. rdlll
 4. dllrl
 5. dllud
 6. ...
이때 dllrl보다 사전 순으로 빠른 경로로 탈출할 수는 없습니다.

격자의 크기를 뜻하는 정수 n, m, 출발 위치를 뜻하는 정수 x, y, 탈출 지점을 뜻하는 정수 r, c, 탈출까지 이동해야 하는 거리를 뜻하는 정수 k가 매개변수로 주어집니다. 이때, 미로를 탈출하기 위한 경로를 return 하도록 solution 함수를 완성해주세요. 단, 위 조건대로 미로를 탈출할 수 없는 경우 "impossible"을 return 해야 합니다.

***

### 제한사항

 - 2 ≤ n (= 미로의 세로 길이) ≤ 50
 - 2 ≤ m (= 미로의 가로 길이) ≤ 50
 - 1 ≤ x ≤ n
 - 1 ≤ y ≤ m
 - 1 ≤ r ≤ n
 - 1 ≤ c ≤ m
 - (x, y) ≠ (r, c)
 - 1 ≤ k ≤ 2,500

***

### 답안
``` csharp
using System;
using System.Text;

public class Solution {
    public string solution(int n, int m, int x, int y, int r, int c, int k) {
        StringBuilder sb = new StringBuilder(k);
        
        if(Math.Abs(r - x) + Math.Abs(c - y) > k || Math.Abs(((r - x) + (c - y)) % 2) != k % 2) {
            return "impossible";
        }
        
        int currentX = x;
        int currentY = y;
        int remaining = k;

        for(int i = 0; i < k; i++) {
            if(Math.Abs(r - currentX) + Math.Abs(c - currentY) == remaining) {
                if(currentX < r) {
                    sb.Append('d');
                    currentX++;
                }else if(currentY > c) {
                    sb.Append('l');
                    currentY--;
                }else if(currentY < c) {
                    sb.Append('r');
                    currentY++;
                }else if(currentX > r) {
                    sb.Append('u');
                    currentX--;
                }
            }else{
                if(currentX != n) {
                    sb.Append('d');
                    currentX++;
                }else if(currentY != 1) {
                    sb.Append('l');
                    currentY--;
                }else{
                    sb.Append('r');
                    currentY++;
                }
            }
            remaining--;      
        }
        
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.42ms, 30.6MB)
테스트 2 〉	통과 (0.41ms, 31MB)
테스트 3 〉	통과 (0.39ms, 31.1MB)
테스트 4 〉	통과 (0.40ms, 30.9MB)
테스트 5 〉	통과 (0.44ms, 30.8MB)
테스트 6 〉	통과 (0.40ms, 31MB)
테스트 7 〉	통과 (0.40ms, 30.7MB)
테스트 8 〉	통과 (0.40ms, 31MB)
테스트 9 〉	통과 (0.45ms, 30.8MB)
테스트 10 〉	통과 (0.43ms, 31MB)
테스트 11 〉	통과 (0.42ms, 31MB)
테스트 12 〉	통과 (0.43ms, 31.2MB)
테스트 13 〉	통과 (0.41ms, 30.9MB)
테스트 14 〉	통과 (0.42ms, 31.2MB)
테스트 15 〉	통과 (0.42ms, 31.2MB)
테스트 16 〉	통과 (0.45ms, 31.3MB)
테스트 17 〉	통과 (0.45ms, 31.1MB)
테스트 18 〉	통과 (0.42ms, 30.9MB)
테스트 19 〉	통과 (0.44ms, 31.1MB)
테스트 20 〉	통과 (0.46ms, 31.2MB)
테스트 21 〉	통과 (0.48ms, 31.1MB)
테스트 22 〉	통과 (0.42ms, 31MB)
테스트 23 〉	통과 (0.42ms, 30.8MB)
테스트 24 〉	통과 (0.43ms, 31.3MB)
테스트 25 〉	통과 (0.47ms, 31MB)
테스트 26 〉	통과 (0.44ms, 30.9MB)
테스트 27 〉	통과 (0.42ms, 31.2MB)
테스트 28 〉	통과 (0.48ms, 31.2MB)
테스트 29 〉	통과 (0.44ms, 31.1MB)
테스트 30 〉	통과 (0.42ms, 31.4MB)
테스트 31 〉	통과 (0.40ms, 30.8MB)
```