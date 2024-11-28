# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43162">네트워크</a>

### 문제설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

***

### 제한사항

 - 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
 - 각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
 - i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
 - computer[i][i]는 항상 1입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int answer;
    int count;
    bool[] visit;
    public int solution(int n, int[,] computers) {
        if(n == 1) return 1;
        answer = 0;
        count = n;
        visit = new bool[count];
        for(int i = 0; i < count; i++) {
            dfs(computers, i, 0);
        }
        return answer;
    }
    void dfs(int[,] _computers, int _index, int _depth) {
        if(visit[_index]) return;
        visit[_index] = true;
        for(int i = 0; i < count; i++) {
            if(visit[i]) continue;
            if(_index == i) continue;
            if(_computers[_index,i] == 0) continue;
            dfs(_computers, i, _depth + 1);
        }
        if(_depth == 0) {
            answer++;
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.26ms, 31.5MB)
테스트 2 〉	통과 (0.25ms, 31.4MB)
테스트 3 〉	통과 (0.26ms, 31.5MB)
테스트 4 〉	통과 (0.26ms, 31.5MB)
테스트 5 〉	통과 (0.19ms, 31.6MB)
테스트 6 〉	통과 (0.28ms, 31.6MB)
테스트 7 〉	통과 (0.27ms, 31.7MB)
테스트 8 〉	통과 (0.26ms, 31.4MB)
테스트 9 〉	통과 (0.26ms, 31.2MB)
테스트 10 〉	통과 (0.25ms, 31.4MB)
테스트 11 〉	통과 (0.31ms, 31.7MB)
테스트 12 〉	통과 (0.29ms, 31.6MB)
테스트 13 〉	통과 (0.29ms, 31.6MB)
```