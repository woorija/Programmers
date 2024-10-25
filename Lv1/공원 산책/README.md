# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/172928">공원 산책</a>

### 문제설명

지나다니는 길을 'O', 장애물을 'X'로 나타낸 직사각형 격자 모양의 공원에서 로봇 강아지가 산책을 하려합니다. 산책은 로봇 강아지에 미리 입력된 명령에 따라 진행하며, 명령은 다음과 같은 형식으로 주어집니다.

 - ["방향 거리", "방향 거리" … ]

예를 들어 "E 5"는 로봇 강아지가 현재 위치에서 동쪽으로 5칸 이동했다는 의미입니다. 로봇 강아지는 명령을 수행하기 전에 다음 두 가지를 먼저 확인합니다.

 - 주어진 방향으로 이동할 때 공원을 벗어나는지 확인합니다.
 - 주어진 방향으로 이동 중 장애물을 만나는지 확인합니다.

위 두 가지중 어느 하나라도 해당된다면, 로봇 강아지는 해당 명령을 무시하고 다음 명령을 수행합니다.

공원의 가로 길이가 W, 세로 길이가 H라고 할 때, 공원의 좌측 상단의 좌표는 (0, 0), 우측 하단의 좌표는 (H - 1, W - 1) 입니다.


공원을 나타내는 문자열 배열 park, 로봇 강아지가 수행할 명령이 담긴 문자열 배열 routes가 매개변수로 주어질 때, 로봇 강아지가 모든 명령을 수행 후 놓인 위치를 [세로 방향 좌표, 가로 방향 좌표] 순으로 배열에 담아 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 3 ≤ park의 길이 ≤ 50
   - 3 ≤ park[i]의 길이 ≤ 50
     - park[i]는 다음 문자들로 이루어져 있으며 시작지점은 하나만 주어집니다.
       - S : 시작 지점
       - O : 이동 가능한 통로
       - X : 장애물
   - park는 직사각형 모양입니다.
 - 1 ≤ routes의 길이 ≤ 50
   - routes의 각 원소는 로봇 강아지가 수행할 명령어를 나타냅니다.
   - 로봇 강아지는 routes의 첫 번째 원소부터 순서대로 명령을 수행합니다.
   - routes의 원소는 "op n"과 같은 구조로 이루어져 있으며, op는 이동할 방향, n은 이동할 칸의 수를 의미합니다.
     - op는 다음 네 가지중 하나로 이루어져 있습니다.
       - N : 북쪽으로 주어진 칸만큼 이동합니다.
       - S : 남쪽으로 주어진 칸만큼 이동합니다.
       - W : 서쪽으로 주어진 칸만큼 이동합니다.
       - E : 동쪽으로 주어진 칸만큼 이동합니다.
     - 1 ≤ n ≤ 9

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(string[] park, string[] routes) {
        int[] answer = new int[2];
        int[] dirX = new int[4] { 1, 0, -1, 0 };
        int[] dirY = new int[4] { 0, 1, 0, -1 };
        int row = park[0].Length;
        int col = park.Length;
        int currentX = 0;
        int currentY = 0;
        int dir = 0;
        
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                int index = park[i].IndexOf("S");
                if(index != -1) {
                    currentX = index;
                    currentY = i;
                }
            }
        }
        
        for(int i = 0; i < routes.Length; i++) {
            string[] str = routes[i].Split(" ");
            int count = int.Parse(str[1]);
            
            switch(str[0]) {
                case "W":
                    dir = 2;
                    break;
                case "E":
                    dir = 0;
                    break;
                case "N":
                    dir = 3;
                    break;
                case "S":
                    dir = 1;
                    break;
            }
            
            int tempX = currentX;
            int tempY = currentY;
            bool check = true;
            
            for(int j = 0; j < count; j++) {
                tempX += dirX[dir];
                tempY += dirY[dir];
                if(tempX < 0 || tempX >= row || tempY < 0 || tempY >= col) {
                    check = false;
                    break;
                } 
                if(park[tempY][tempX] == 'X') {
                    check = false;
                    break;
                }
            }
            if(check) {
                currentX = tempX;
                currentY = tempY;
            }
        }
        
        answer[0] = currentY;
        answer[1] = currentX;
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.36ms, 31.7MB)
테스트 2 〉	통과 (3.38ms, 31.6MB)
테스트 3 〉	통과 (4.12ms, 31.7MB)
테스트 4 〉	통과 (3.62ms, 31.6MB)
테스트 5 〉	통과 (3.83ms, 31.6MB)
테스트 6 〉	통과 (4.44ms, 32.1MB)
테스트 7 〉	통과 (4.30ms, 31.9MB)
테스트 8 〉	통과 (4.37ms, 31.5MB)
테스트 9 〉	통과 (4.73ms, 31.6MB)
테스트 10 〉	통과 (5.91ms, 31.8MB)
테스트 11 〉	통과 (6.86ms, 31.8MB)
테스트 12 〉	통과 (4.34ms, 31.8MB)
테스트 13 〉	통과 (4.25ms, 31.9MB)
테스트 14 〉	통과 (4.31ms, 31.6MB)
테스트 15 〉	통과 (4.27ms, 31.8MB)
테스트 16 〉	통과 (3.66ms, 31.6MB)
테스트 17 〉	통과 (4.92ms, 31.9MB)
테스트 18 〉	통과 (3.78ms, 31.1MB)
테스트 19 〉	통과 (5.10ms, 31.8MB)
테스트 20 〉	통과 (5.33ms, 32MB)
```