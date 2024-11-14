# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12952">N-Queen</a>

### 문제설명

가로, 세로 길이가 n인 정사각형으로된 체스판이 있습니다. 체스판 위의 n개의 퀸이 서로를 공격할 수 없도록 배치하고 싶습니다.

체스판의 가로 세로의 세로의 길이 n이 매개변수로 주어질 때, n개의 퀸이 조건에 만족 하도록 배치할 수 있는 방법의 수를 return하는 solution함수를 완성해주세요.

***

### 제한사항

 - 퀸(Queen)은 가로, 세로, 대각선으로 이동할 수 있습니다.
 - n은 12이하의 자연수 입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int answer;
    int num;
    int[] board;
    bool[] used;
    
    public int solution(int n) {
        answer = 0;
        num = n;
        board = new int[n];
        used = new bool[n];

        for(int i = 0; i < n; i++) {
            board[i] = -1;
        }
        
        for(int i = 0; i < n; i++) {
            dfs(0, i);
        }
        
        return answer;
    }
    
    void dfs(int _index, int _num) {
        if(used[_num]) {
            return;
        }
        
        used[_num] = true;
        board[_index] = _num;
        
        for(int i = 0; i < num; i++) {
            if(i == _index || board[i] == -1) continue;
            
            int temp = Math.Abs(i - _index);
            int temp2 = Math.Abs(board[i] - board[_index]);
            
            if(temp == temp2) {
                used[_num] = false;
                board[_index] = -1;
                return;
            }

        }
        
        if(_index + 1 == num) {
            used[_num] = false;
            board[_index] = -1;
            answer++;
            return;
        }
        
        for(int i = 0; i < num; i++) {
            dfs(_index + 1, i);
        }
        
        used[_num] = false;
        board[_index] = -1;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.37ms, 31.4MB)
테스트 2 〉	통과 (0.38ms, 31.3MB)
테스트 3 〉	통과 (0.49ms, 31.5MB)
테스트 4 〉	통과 (0.57ms, 31.5MB)
테스트 5 〉	통과 (0.39ms, 31.4MB)
테스트 6 〉	통과 (0.53ms, 31.1MB)
테스트 7 〉	통과 (0.84ms, 31.4MB)
테스트 8 〉	통과 (1.86ms, 31.1MB)
테스트 9 〉	통과 (7.46ms, 31.4MB)
테스트 10 〉	통과 (36.68ms, 31.4MB)
테스트 11 〉	통과 (229.51ms, 31.6MB)
```