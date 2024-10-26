# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43164">여행경로</a>

### 문제설명

주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 "ICN" 공항에서 출발합니다.

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때, 방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
 - 주어진 공항 수는 3개 이상 10,000개 이하입니다.
 - tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
 - 주어진 항공권은 모두 사용해야 합니다.
 - 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
 - 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Ticket : IComparable<Ticket> {
    public string from;
    public string to;
    
    public Ticket(string _from, string _to) {
        from = _from;
        to = _to;
    }
    
    int IComparable<Ticket>.CompareTo(Ticket _other) {
        int result = from.CompareTo(_other.from);
        if(result == 0) {
            result = to.CompareTo(_other.to);
        }
        return result;
    }
}

public class Solution {
    string[] answer;
    List<Ticket> list;
    bool[] used;
    public string[] solution(string[,] tickets) {
        list = new List<Ticket>();
        int length = tickets.GetLength(0);
        answer = new string[length + 1];
        
        for(int i = 0; i < length; i++) {
            list.Add(new Ticket(tickets[i,0], tickets[i,1]));
        }
        used = new bool[list.Count];
        list.Sort();
        
        dfs("ICN",0);

        return answer;
    }
    bool dfs(string _current, int _index) {
        
        if(_index == answer.Length - 1) {
            answer[_index] = _current;
            return false;
        }
        
        int currentIndex = 0;
        bool flag = true;
        
        while(true) {
            int nextIndex = IndexOfList(_current, currentIndex);
            if(nextIndex == -1) {
                break;
            }
            if(!used[nextIndex]) {
                answer[_index] = list[nextIndex].from;
                used[nextIndex] = true;
                flag = dfs(list[nextIndex].to, _index + 1);
                used[nextIndex] = false;
            }
            if(!flag) {
                break;
            }
            currentIndex = nextIndex + 1;
        }
        return flag;
    }
    
    int IndexOfList(string str, int _startIndex) {
        int index = -1;
        for(int i = _startIndex; i < list.Count; i++) {
            if(list[i].from == str) {
                index = i;
                break;
            }
        }
        return index;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (4.16ms, 31.8MB)
테스트 2 〉	통과 (3.95ms, 31.6MB)
테스트 3 〉	통과 (3.94ms, 31.5MB)
테스트 4 〉	통과 (4.12ms, 31.7MB)
```