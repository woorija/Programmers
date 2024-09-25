# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/155651">호텔 대실</a>

### 문제설명

호텔을 운영 중인 코니는 최소한의 객실만을 사용하여 예약 손님들을 받으려고 합니다. 한 번 사용한 객실은 퇴실 시간을 기준으로 10분간 청소를 하고 다음 손님들이 사용할 수 있습니다.

예약 시각이 문자열 형태로 담긴 2차원 배열 book_time이 매개변수로 주어질 때, 코니에게 필요한 최소 객실의 수를 return 하는 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ book_time의 길이 ≤ 1,000
   - book_time[i]는 ["HH:MM", "HH:MM"]의 형태로 이루어진 배열입니다
     - [대실 시작 시각, 대실 종료 시각] 형태입니다.
   - 시각은 HH:MM 형태로 24시간 표기법을 따르며, "00:00" 부터 "23:59" 까지로 주어집니다.
     - 예약 시각이 자정을 넘어가는 경우는 없습니다.
     - 시작 시각은 항상 종료 시각보다 빠릅니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(string[,] book_time) {
        int answer = 0;
        int length = book_time.GetLength(0);
        int[] enterTimes = new int[length];
        int[] exitTimes = new int[length];
        List<int> list = new List<int>();
        list.Add(-1);
        for(int i = 0; i < length; i++) {
            string[] enter = book_time[i,0].Split(":");
            enterTimes[i] = int.Parse(enter[0]) * 60 + int.Parse(enter[1]);
            string[] exit = book_time[i,1].Split(":");
            exitTimes[i] = int.Parse(exit[0]) * 60 + int.Parse(exit[1]) + 9;
        }
        Array.Sort(enterTimes, exitTimes);
        for(int i = 0; i < length; i++) {
            list.Sort();
            int check = -1;
            for(int j = 0; j < list.Count; j++) {
                if(enterTimes[i] > list[j]) {
                    check = j;
                    break;
                }
            }
            if(check == -1) {
                list.Add(exitTimes[i]);
            }else{
                list[check] = exitTimes[i];
            }
        }
        answer = list.Count;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.81ms, 31.5MB)
테스트 2 〉	통과 (4.20ms, 31.8MB)
테스트 3 〉	통과 (16.24ms, 32MB)
테스트 4 〉	통과 (7.05ms, 31.8MB)
테스트 5 〉	통과 (1.53ms, 31.3MB)
테스트 6 〉	통과 (12.92ms, 32.2MB)
테스트 7 〉	통과 (14.19ms, 31.8MB)
테스트 8 〉	통과 (5.33ms, 31.6MB)
테스트 9 〉	통과 (4.45ms, 31.8MB)
테스트 10 〉	통과 (8.89ms, 31.9MB)
테스트 11 〉	통과 (19.78ms, 32.2MB)
테스트 12 〉	통과 (17.09ms, 32.1MB)
테스트 13 〉	통과 (4.02ms, 31.8MB)
테스트 14 〉	통과 (13.29ms, 32.1MB)
테스트 15 〉	통과 (16.37ms, 32.2MB)
테스트 16 〉	통과 (5.30ms, 31.8MB)
테스트 17 〉	통과 (19.63ms, 32.1MB)
테스트 18 〉	통과 (9.52ms, 32MB)
테스트 19 〉	통과 (28.22ms, 32.3MB)
```