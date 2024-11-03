# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/81302">거리두기 확인하기</a>

### 문제설명

개발자를 희망하는 죠르디가 카카오에 면접을 보러 왔습니다.

코로나 바이러스 감염 예방을 위해 응시자들은 거리를 둬서 대기를 해야하는데 개발 직군 면접인 만큼
아래와 같은 규칙으로 대기실에 거리를 두고 앉도록 안내하고 있습니다.

```
 1. 대기실은 5개이며, 각 대기실은 5x5 크기입니다.
 2. 거리두기를 위하여 응시자들 끼리는 맨해튼 거리1가 2 이하로 앉지 말아 주세요.
 3. 단 응시자가 앉아있는 자리 사이가 파티션으로 막혀 있을 경우에는 허용합니다.
```

5개의 대기실을 본 죠르디는 각 대기실에서 응시자들이 거리두기를 잘 기키고 있는지 알고 싶어졌습니다. 자리에 앉아있는 응시자들의 정보와 대기실 구조를 대기실별로 담은 2차원 문자열 배열 places가 매개변수로 주어집니다. 각 대기실별로 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

***

### 제한사항

 - places의 행 길이(대기실 개수) = 5
   - places의 각 행은 하나의 대기실 구조를 나타냅니다.
 - places의 열 길이(대기실 세로 길이) = 5
 - places의 원소는 P,O,X로 이루어진 문자열입니다.
   - places 원소의 길이(대기실 가로 길이) = 5
   - P는 응시자가 앉아있는 자리를 의미합니다.
   - O는 빈 테이블을 의미합니다.
   - X는 파티션을 의미합니다.
 - 입력으로 주어지는 5개 대기실의 크기는 모두 5x5 입니다.
 - return 값 형식
   - 1차원 정수 배열에 5개의 원소를 담아서 return 합니다.
   - places에 담겨 있는 5개 대기실의 순서대로, 거리두기 준수 여부를 차례대로 배열에 담습니다.
   - 각 대기실 별로 모든 응시자가 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 담습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public struct Pos {
    public int x;
    public int y;
    public Pos(int _x, int _y) {
        x = _x;
        y = _y;
    }
}

public class Solution {
    public int[] solution(string[,] places) {
        int[] answer = new int[5];
        
        for(int i = 0; i < 5; i++) {
            answer[i] = 1;
        }
        
        for(int i = 0; i < 5; i++) {
            bool flag = false;
            List<Pos> list = new List<Pos>();
            
            for(int j = 0; j < 5; j++) {
                for(int k = 0; k < 5; k++) {
                    if(places[i,j][k] == 'P') {
                        list.Add(new Pos(k, j));
                    }
                }
            }
            
            for(int j = 0; j < list.Count - 1; j++) {
                for(int k = j + 1; k < list.Count; k++) {
                    
                    if(GetLength(list[j], list[k]) < 2) {
                        answer[i] = 0;
                        flag = true;
                        break;
                    }
                    
                    if(GetLength(list[j], list[k]) == 2) {
                        if(list[j].x == list[k].x) {
                            int temp = Math.Max(list[j].y, list[k].y) - 1;
                            if(places[i,temp][list[j].x] == 'O') {
                                answer[i] = 0;
                                flag = true;
                                break;
                            }
                        }else if(list[j].y == list[k].y) {
                            int temp = Math.Max(list[j].x, list[k].x) - 1;
                            if(places[i,list[j].y][temp] == 'O') {
                                answer[i] = 0;
                                flag = true;
                                break;
                            }
                        }else{
                            if(places[i,list[j].y][list[k].x] == 'O' || places[i,list[k].y][list[j].x] == 'O') {
                                answer[i] = 0;
                                flag = true;
                                break;
                            }
                        }
                    }
                }
                if(flag) {
                    break;
                }
            }
        }
        return answer;
    }
    
    int GetLength(Pos pos1, Pos pos2) {
        return Math.Abs(pos1.x - pos2.x) + Math.Abs(pos1.y - pos2.y);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.57ms, 31.2MB)
테스트 2 〉	통과 (1.37ms, 31MB)
테스트 3 〉	통과 (1.33ms, 31.1MB)
테스트 4 〉	통과 (1.56ms, 31.3MB)
테스트 5 〉	통과 (1.61ms, 31.1MB)
테스트 6 〉	통과 (1.31ms, 31.1MB)
테스트 7 〉	통과 (1.34ms, 31.2MB)
테스트 8 〉	통과 (1.59ms, 31.1MB)
테스트 9 〉	통과 (1.60ms, 31.4MB)
테스트 10 〉	통과 (1.32ms, 31.2MB)
테스트 11 〉	통과 (1.34ms, 31.4MB)
테스트 12 〉	통과 (1.51ms, 31.2MB)
테스트 13 〉	통과 (1.90ms, 30.8MB)
테스트 14 〉	통과 (1.32ms, 31.3MB)
테스트 15 〉	통과 (1.56ms, 31.1MB)
테스트 16 〉	통과 (1.59ms, 31.1MB)
테스트 17 〉	통과 (1.56ms, 31.3MB)
테스트 18 〉	통과 (1.54ms, 31.4MB)
테스트 19 〉	통과 (1.59ms, 30.9MB)
테스트 20 〉	통과 (1.35ms, 31.6MB)
테스트 21 〉	통과 (1.35ms, 31.3MB)
테스트 22 〉	통과 (1.31ms, 31.2MB)
테스트 23 〉	통과 (1.12ms, 31.2MB)
테스트 24 〉	통과 (1.58ms, 31.1MB)
테스트 25 〉	통과 (0.97ms, 31.1MB)
테스트 26 〉	통과 (1.12ms, 31.1MB)
테스트 27 〉	통과 (1.34ms, 31.3MB)
테스트 28 〉	통과 (1.52ms, 31.2MB)
테스트 29 〉	통과 (1.32ms, 31.5MB)
테스트 30 〉	통과 (1.67ms, 31.3MB)
테스트 31 〉	통과 (1.56ms, 31.2MB)
```