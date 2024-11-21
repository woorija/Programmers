# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87377">교점에 별 만들기</a>

### 문제설명

Ax + By + C = 0으로 표현할 수 있는 n개의 직선이 주어질 때, 이 직선의 교점 중 정수 좌표에 별을 그리려 합니다.

예를 들어, 다음과 같은 직선 5개가 있습니다.

```
 - 2x - y + 4 = 0
 - -2x - y + 4 = 0
 - -y + 1 = 0
 - 5x - 8y - 12 = 0
 - 5x + 8y + 12 = 0
```

이때, 모든 교점의 좌표는 (4, 1), (4, -4), (-4, -4), (-4, 1), (0, 4), (1.5, 1.0), (2.1, -0.19), (0, -1.5), (-2.1, -0.19), (-1.5, 1.0)입니다. 

이 중 정수로만 표현되는 좌표는 (4, 1), (4, -4), (-4, -4), (-4, 1), (0, 4)입니다.

교점인 부분은 *, 빈 공간은 .으로 표현하면 다음과 같습니다.

```
"..........."  
".....*....."  
"..........."  
"..........."  
".*.......*."  
"..........."  
"..........."  
"..........."  
"..........."  
".*.......*."  
"..........."  
```

이때 격자판은 무한히 넓으니 모든 별을 포함하는 최소한의 크기만 나타내면 됩니다.

따라서 정답은
```
"....*...."  
"........."  
"........."  
"*.......*"  
"........."  
"........."  
"........."  
"........."  
"*.......*"
```  
입니다.

직선 A, B, C에 대한 정보가 담긴 배열 line이 매개변수로 주어집니다. 이때 모든 별을 포함하는 최소 사각형을 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - line의 세로(행) 길이는 2 이상 1,000 이하인 자연수입니다.
   - line의 가로(열) 길이는 3입니다.
   - line의 각 원소는 [A, B, C] 형태입니다.
   - A, B, C는 -100,000 이상 100,000 이하인 정수입니다.
   - 무수히 많은 교점이 생기는 직선 쌍은 주어지지 않습니다.
   - A = 0이면서 B = 0인 경우는 주어지지 않습니다.
 - 정답은 1,000 * 1,000 크기 이내에서 표현됩니다.
 - 별이 한 개 이상 그려지는 입력만 주어집니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;
using System.Text;

public class Solution {
    public string[] solution(int[,] line) {
        string[] answer;
        Dictionary<long, List<long>> map = new Dictionary<long, List<long>>();
        long maxX = long.MinValue;
        long maxY = long.MinValue;
        long minX = long.MaxValue;
        long minY = long.MaxValue;
        
        for(int i = 0; i < line.GetLength(0) - 1; i++) {
            for(int j = i + 1; j < line.GetLength(0); j++) {
                long div = (long)line[i,0] * line[j,1] - (long)line[i,1] * line[j,0];
                long divX = (long)line[i,1] * line[j,2] - (long)line[i,2] * line[j,1];
                long divY = (long)line[i,2] * line[j,0] - (long)line[i,0] * line[j,2];
                
                if(div !=0  && divX % div == 0 && divY % div == 0) {
                    long x = divX / div;
                    long y = divY / div;
                    
                    maxX = Math.Max(maxX, x);
                    maxY = Math.Max(maxY, y);
                    minX = Math.Min(minX, x);
                    minY = Math.Min(minY, y);
                    
                    if(!map.ContainsKey(y)) {
                        map[y] = new List<long>();
                    }
                    map[y].Add(x);
                }
            }
        }
        
        answer = new string[maxY - minY + 1];
        StringBuilder sb = new StringBuilder();
        
        for(long i = maxY; i >= minY; i--) {
            sb.Clear();
            
            if(map.ContainsKey(i)) {
                for(long j = minX; j <= maxX; j++) {
                    if(map[i].Contains(j)) {
                        sb.Append('*');
                    }else{
                        sb.Append('.');
                    }
                }
            }else{
                for(long j = minX; j <= maxX; j++) {
                    sb.Append('.');
                }
            }
            answer[maxY - i] = sb.ToString();
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.73ms, 31.1MB)
테스트 2 〉	통과 (4.41ms, 32.1MB)
테스트 3 〉	통과 (2.73ms, 31.4MB)
테스트 4 〉	통과 (5.48ms, 33.8MB)
테스트 5 〉	통과 (3.86ms, 31.5MB)
테스트 6 〉	통과 (3.18ms, 31.4MB)
테스트 7 〉	통과 (3.80ms, 32.2MB)
테스트 8 〉	통과 (2.82ms, 30.8MB)
테스트 9 〉	통과 (12.06ms, 31.4MB)
테스트 10 〉	통과 (12.98ms, 31MB)
테스트 11 〉	통과 (14.21ms, 31.3MB)
테스트 12 〉	통과 (16.55ms, 31.4MB)
테스트 13 〉	통과 (16.87ms, 31.1MB)
테스트 14 〉	통과 (22.21ms, 31.4MB)
테스트 15 〉	통과 (14.71ms, 31.4MB)
테스트 16 〉	통과 (13.25ms, 31.4MB)
테스트 17 〉	통과 (15.20ms, 31.9MB)
테스트 18 〉	통과 (16.28ms, 31.2MB)
테스트 19 〉	통과 (14.46ms, 31.3MB)
테스트 20 〉	통과 (12.03ms, 31MB)
테스트 21 〉	통과 (13.19ms, 32.1MB)
테스트 22 〉	통과 (2.71ms, 31.4MB)
테스트 23 〉	통과 (2.71ms, 31.4MB)
테스트 24 〉	통과 (3.03ms, 31.4MB)
테스트 25 〉	통과 (2.77ms, 31.2MB)
테스트 26 〉	통과 (2.86ms, 31.2MB)
테스트 27 〉	통과 (3.02ms, 31MB)
테스트 28 〉	통과 (2.74ms, 31.2MB)
테스트 29 〉	통과 (2.73ms, 31.3MB)
```