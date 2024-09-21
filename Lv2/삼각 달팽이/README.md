# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/68645">삼각 달팽이</a>

### 문제설명

정수 n이 매개변수로 주어집니다. 다음 그림과 같이 밑변의 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - n은 1 이상 1,000 이하입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int n) {
        List<int> answer = new List<int>();
        int[,] tri = new int[n,n];
        int indexX = 0;
        int indexY = -1;
        int dir = 0;
        int[] dirX = new int[3] { 0, 1, -1 };
        int[] dirY = new int[3] { 1, 0, -1 };
        
        int count = 0;
        int value = 1;
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= n - count; j++) {
                indexX += dirX[dir];
                indexY += dirY[dir];
                tri[indexX,indexY] = value;
                value++;
            }
            dir = (dir + 1) % 3;
            count++;
        }
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < n; j++) {
                if(tri[j,i] != 0) {
                    answer.Add(tri[j,i]);
                }
            }
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.72ms, 31.1MB)
테스트 2 〉	통과 (0.71ms, 31.1MB)
테스트 3 〉	통과 (0.70ms, 30.9MB)
테스트 4 〉	통과 (1.19ms, 31.2MB)
테스트 5 〉	통과 (0.85ms, 31.2MB)
테스트 6 〉	통과 (1.33ms, 31.3MB)
테스트 7 〉	통과 (14.38ms, 57MB)
테스트 8 〉	통과 (14.00ms, 57.1MB)
테스트 9 〉	통과 (13.22ms, 57.5MB)
```