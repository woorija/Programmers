# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/154540">무인도 여행</a>

### 문제설명

메리는 여름을 맞아 무인도로 여행을 가기 위해 지도를 보고 있습니다. 지도에는 바다와 무인도들에 대한 정보가 표시돼 있습니다. 지도는 1 x 1크기의 사각형들로 이루어진 직사각형 격자 형태이며, 격자의 각 칸에는 'X' 또는 1에서 9 사이의 자연수가 적혀있습니다. 지도의 'X'는 바다를 나타내며, 숫자는 무인도를 나타냅니다. 이때, 상, 하, 좌, 우로 연결되는 땅들은 하나의 무인도를 이룹니다. 지도의 각 칸에 적힌 숫자는 식량을 나타내는데, 상, 하, 좌, 우로 연결되는 칸에 적힌 숫자를 모두 합한 값은 해당 무인도에서 최대 며칠동안 머물 수 있는지를 나타냅니다. 어떤 섬으로 놀러 갈지 못 정한 메리는 우선 각 섬에서 최대 며칠씩 머물 수 있는지 알아본 후 놀러갈 섬을 결정하려 합니다.

지도를 나타내는 문자열 배열 maps가 매개변수로 주어질 때, 각 섬에서 최대 며칠씩 머무를 수 있는지 배열에 오름차순으로 담아 return 하는 solution 함수를 완성해주세요. 만약 지낼 수 있는 무인도가 없다면 -1을 배열에 담아 return 해주세요.

***

### 제한사항

 - 3 ≤ maps의 길이 ≤ 100
   - 3 ≤ maps[i]의 길이 ≤ 100
   - maps[i]는 'X' 또는 1 과 9 사이의 자연수로 이루어진 문자열입니다.
   - 지도는 직사각형 형태입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    List<int> answer;
    HashSet<(int,int)> visit;
    int row;
    int col;
    
    public int[] solution(string[] maps) {
        answer = new List<int>();
        visit = new HashSet<(int,int)>();
        row = maps[0].Length;
        col = maps.Length;
        
        for(int i = 0; i < row; i++) {
            for(int j = 0; j < col; j++) {
                int temp = dfs(maps, i, j);
                if(temp != 0) {
                    answer.Add(temp);
                }
            }
        }
        
        if(answer.Count == 0) {
            answer.Add(-1);
        }
        answer.Sort();
        return answer.ToArray();
    }
    int dfs(string[] _maps, int _x, int _y) {
        if(visit.Contains((_x,_y))) return 0;
        visit.Add((_x,_y));
        if(_x == -1 || _y == -1 || _x == row || _y == col) return 0;
        if(_maps[_y][_x] == 'X') return 0;
        int num = int.Parse(_maps[_y][_x].ToString());
        int sum = num;
        int temp = 0;
        temp += dfs(_maps, _x - 1, _y);
        temp += dfs(_maps, _x + 1 ,_y);
        temp += dfs(_maps, _x, _y - 1);
        temp += dfs(_maps, _x, _y + 1);
        sum += temp;
        return sum;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.66ms, 31.3MB)
테스트 2 〉	통과 (3.17ms, 31.5MB)
테스트 3 〉	통과 (3.20ms, 31.5MB)
테스트 4 〉	통과 (4.25ms, 31.6MB)
테스트 5 〉	통과 (4.95ms, 31.9MB)
테스트 6 〉	통과 (5.07ms, 31.9MB)
테스트 7 〉	통과 (4.56ms, 31.7MB)
테스트 8 〉	통과 (5.21ms, 31.9MB)
테스트 9 〉	통과 (6.02ms, 31.8MB)
테스트 10 〉	통과 (5.66ms, 32.1MB)
테스트 11 〉	통과 (5.73ms, 31.8MB)
테스트 12 〉	통과 (7.01ms, 32.1MB)
테스트 13 〉	통과 (6.60ms, 32MB)
테스트 14 〉	통과 (7.60ms, 32.1MB)
테스트 15 〉	통과 (8.06ms, 32.2MB)
테스트 16 〉	통과 (9.03ms, 32.7MB)
테스트 17 〉	통과 (4.41ms, 31.7MB)
테스트 18 〉	통과 (8.42ms, 32.5MB)
테스트 19 〉	통과 (9.06ms, 32.7MB)
테스트 20 〉	통과 (4.32ms, 31.6MB)
테스트 21 〉	통과 (5.00ms, 31.7MB)
테스트 22 〉	통과 (3.23ms, 31.4MB)
테스트 23 〉	통과 (7.62ms, 32.3MB)
테스트 24 〉	통과 (8.04ms, 32.4MB)
테스트 25 〉	통과 (4.33ms, 31.7MB)
```