# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/176962">과제 진행하기</a>

### 문제설명

과제를 받은 루는 다음과 같은 순서대로 과제를 하려고 계획을 세웠습니다.

 - 과제는 시작하기로 한 시각이 되면 시작합니다.
 - 새로운 과제를 시작할 시각이 되었을 때, 기존에 진행 중이던 과제가 있다면 진행 중이던 과제를 멈추고 새로운 과제를 시작합니다.
 - 진행중이던 과제를 끝냈을 때, 잠시 멈춘 과제가 있다면, 멈춰둔 과제를 이어서 진행합니다.
   - 만약, 과제를 끝낸 시각에 새로 시작해야 되는 과제와 잠시 멈춰둔 과제가 모두 있다면, 새로 시작해야 하는 과제부터 진행합니다.
 - 멈춰둔 과제가 여러 개일 경우, 가장 최근에 멈춘 과제부터 시작합니다.

과제 계획을 담은 이차원 문자열 배열 plans가 매개변수로 주어질 때, 과제를 끝낸 순서대로 이름을 배열에 담아 return 하는 solution 함수를 완성해주세요.

***

### 제한사항

 - 3 ≤ plans의 길이 ≤ 1,000
   - plans의 원소는 [name, start, playtime]의 구조로 이루어져 있습니다.
     - name : 과제의 이름을 의미합니다.
       - 2 ≤ name의 길이 ≤ 10
       - name은 알파벳 소문자로만 이루어져 있습니다.
       - name이 중복되는 원소는 없습니다.
     - start : 과제의 시작 시각을 나타냅니다.
       - "hh:mm"의 형태로 "00:00" ~ "23:59" 사이의 시간값만 들어가 있습니다.
       - 모든 과제의 시작 시각은 달라서 겹칠 일이 없습니다.
       - 과제는 "00:00" ... "23:59" 순으로 시작하면 됩니다. 즉, 시와 분의 값이 작을수록 더 빨리 시작한 과제입니다.
     - playtime : 과제를 마치는데 걸리는 시간을 의미하며, 단위는 분입니다.
       - 1 ≤ playtime ≤ 100
       - playtime은 0으로 시작하지 않습니다.
     - 배열은 시간순으로 정렬되어 있지 않을 수 있습니다.
 - 진행중이던 과제가 끝나는 시각과 새로운 과제를 시작해야하는 시각이 같은 경우 진행중이던 과제는 끝난 것으로 판단합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Assignment : IComparable<Assignment> {
    public string name;
    public int startTime;
    public int remainingTime;
    
    public Assignment(string _name, int _startTime, int _remainingTime) {
        name = _name;
        startTime = _startTime;
        remainingTime = _remainingTime;
    }
    
    public void Play(int _time) {
        remainingTime -= _time;
    }
    
    public bool IsComplete() {
        return remainingTime <= 0;
    }
    
    public int GetRemainingTime() {
        return remainingTime;
    }
    
    int IComparable<Assignment>.CompareTo(Assignment _other) {
        return startTime - _other.startTime;
    }
}

public class Solution {
    public string[] solution(string[,] plans) {
        List<string> answer = new List<string>();
        List<Assignment> list = new List<Assignment>();
        Stack<Assignment> remainings = new Stack<Assignment>();
        int length = plans.GetLength(0);
        
        for(int i = 0; i < length; i++) {
            string[] str = plans[i,1].Split(":");
            int time = int.Parse(str[0]) * 60 + int.Parse(str[1]);
            list.Add(new Assignment(plans[i,0], time, int.Parse(plans[i,2])));
        }
        
        list.Sort();
        
        int index = 0;
        while(index != list.Count) {
            Assignment current = list[index];
            int currentTime = current.startTime;
            int nextTime = index + 1 != list.Count ? list[index + 1].startTime : 1440;
            int playTime = current.remainingTime + currentTime;
            
            if(playTime <= nextTime) {
                answer.Add(current.name);
                int remainingTime = nextTime - playTime;
                
                while(remainings.Count != 0 && remainingTime > 0) {
                    current = remainings.Pop();
                    
                    if(remainingTime >= current.remainingTime) {
                        answer.Add(current.name);
                        remainingTime -= current.remainingTime;
                    }else{
                        current.Play(remainingTime);
                        remainingTime = 0;
                        remainings.Push(current);
                    }
                }
            }else{
                current.Play(nextTime - currentTime);
                remainings.Push(current);
            }
            index++;
        }
        
        while(remainings.Count != 0) {
            Assignment temp = remainings.Pop();
            answer.Add(temp.name);
        }
        
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.16ms, 31.3MB)
테스트 2 〉	통과 (2.34ms, 31.3MB)
테스트 3 〉	통과 (2.35ms, 31.3MB)
테스트 4 〉	통과 (2.16ms, 31.5MB)
테스트 5 〉	통과 (2.26ms, 31.5MB)
테스트 6 〉	통과 (2.78ms, 31.4MB)
테스트 7 〉	통과 (2.77ms, 31.6MB)
테스트 8 〉	통과 (2.48ms, 31.5MB)
테스트 9 〉	통과 (3.58ms, 31.6MB)
테스트 10 〉	통과 (2.40ms, 31.7MB)
테스트 11 〉	통과 (2.97ms, 31.5MB)
테스트 12 〉	통과 (2.77ms, 31.7MB)
테스트 13 〉	통과 (2.81ms, 31.9MB)
테스트 14 〉	통과 (4.29ms, 32.2MB)
테스트 15 〉	통과 (3.28ms, 32.2MB)
테스트 16 〉	통과 (2.38ms, 31.6MB)
테스트 17 〉	통과 (2.37ms, 31.3MB)
테스트 18 〉	통과 (2.67ms, 31.5MB)
테스트 19 〉	통과 (2.57ms, 31.5MB)
테스트 20 〉	통과 (2.49ms, 31.4MB)
테스트 21 〉	통과 (2.53ms, 31.6MB)
```