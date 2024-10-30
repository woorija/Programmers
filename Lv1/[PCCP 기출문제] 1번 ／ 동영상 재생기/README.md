# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/340213">[PCCP 기출문제] 1번 ／ 동영상 재생기</a>

### 문제설명

당신은 동영상 재생기를 만들고 있습니다. 당신의 동영상 재생기는 10초 전으로 이동, 10초 후로 이동, 오프닝 건너뛰기 3가지 기능을 지원합니다. 각 기능이 수행하는 작업은 다음과 같습니다.

 - 10초 전으로 이동: 사용자가 "prev" 명령을 입력할 경우 동영상의 재생 위치를 현재 위치에서 10초 전으로 이동합니다. 현재 위치가 10초 미만인 경우 영상의 처음 위치로 이동합니다. 영상의 처음 위치는 0분 0초입니다.
 - 10초 후로 이동: 사용자가 "next" 명령을 입력할 경우 동영상의 재생 위치를 현재 위치에서 10초 후로 이동합니다. 동영상의 남은 시간이 10초 미만일 경우 영상의 마지막 위치로 이동합니다. 영상의 마지막 위치는 동영상의 길이와 같습니다.
 - 오프닝 건너뛰기: 현재 재생 위치가 오프닝 구간(op_start ≤ 현재 재생 위치 ≤ op_end)인 경우 자동으로 오프닝이 끝나는 위치로 이동합니다.

동영상의 길이를 나타내는 문자열 video_len, 기능이 수행되기 직전의 재생위치를 나타내는 문자열 pos, 오프닝 시작 시각을 나타내는 문자열 op_start, 오프닝이 끝나는 시각을 나타내는 문자열 op_end, 사용자의 입력을 나타내는 1차원 문자열 배열 commands가 매개변수로 주어집니다. 이때 사용자의 입력이 모두 끝난 후 동영상의 위치를 "mm:ss" 형식으로 return 하도록 solution 함수를 완성해 주세요.

***

### 제한사항

 - video_len의 길이 = pos의 길이 = op_start의 길이 = op_end의 길이 = 5
   - video_len, pos, op_start, op_end는 "mm:ss" 형식으로 mm분 ss초를 나타냅니다.
   - 0 ≤ mm ≤ 59
   - 0 ≤ ss ≤ 59
   - 분, 초가 한 자리일 경우 0을 붙여 두 자리로 나타냅니다.
   - 비디오의 현재 위치 혹은 오프닝이 끝나는 시각이 동영상의 범위 밖인 경우는 주어지지 않습니다.
   - 오프닝이 시작하는 시각은 항상 오프닝이 끝나는 시각보다 전입니다.
 - 1 ≤ commands의 길이 ≤ 100
   - commands의 원소는 "prev" 혹은 "next"입니다.
   - "prev"는 10초 전으로 이동하는 명령입니다.
   - "next"는 10초 후로 이동하는 명령입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int start;
    int end;
    int last;
    public string solution(string video_len, string pos, string op_start, string op_end, string[] commands) {
        int current = ChangeTime(pos);
        start = ChangeTime(op_start);
        end = ChangeTime(op_end);
        last = ChangeTime(video_len);
        
        current = MoveTime(current);
        for(int i = 0; i < commands.Length; i++) {
            if(commands[i].Equals("prev")) {
                current = MoveTime(current - 10);
            }else{
                current = MoveTime(current + 10);
            }
        }
        return ChangeString(current);
    }
    
    int MoveTime(int _time) {
        int time = Math.Max(0, _time);
        time = Math.Min(time,last);
        if(start <= time && time <= end) {
            return end;
        }
        return time;
    }
    
    int ChangeTime(string _str) {
        string[] arr = _str.Split(":");
        int time = int.Parse(arr[0]) * 60 + int.Parse(arr[1]);
        return time;
    }
    
    string ChangeString(int _time) {
        int min = _time / 60;
        int sec = _time % 60;
        string str = min.ToString("D2") + ":" + sec.ToString("D2");
        return str;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.05ms, 31.4MB)
테스트 2 〉	통과 (1.05ms, 31.2MB)
테스트 3 〉	통과 (1.58ms, 31.3MB)
테스트 4 〉	통과 (1.05ms, 31.4MB)
테스트 5 〉	통과 (1.56ms, 31.2MB)
테스트 6 〉	통과 (1.01ms, 31.4MB)
테스트 7 〉	통과 (0.98ms, 31.5MB)
테스트 8 〉	통과 (1.10ms, 31.3MB)
테스트 9 〉	통과 (1.02ms, 31.5MB)
테스트 10 〉	통과 (1.01ms, 31.2MB)
테스트 11 〉	통과 (0.95ms, 31.1MB)
테스트 12 〉	통과 (0.98ms, 31.3MB)
테스트 13 〉	통과 (1.01ms, 31.3MB)
테스트 14 〉	통과 (1.53ms, 31.7MB)
```