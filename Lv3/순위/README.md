# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49191">순위</a>

### 문제설명

n명의 권투선수가 권투 대회에 참여했고 각각 1번부터 n번까지 번호를 받았습니다. 권투 경기는 1대1 방식으로 진행이 되고, 만약 A 선수가 B 선수보다 실력이 좋다면 A 선수는 B 선수를 항상 이깁니다. 심판은 주어진 경기 결과를 가지고 선수들의 순위를 매기려 합니다. 하지만 몇몇 경기 결과를 분실하여 정확하게 순위를 매길 수 없습니다.

선수의 수 n, 경기 결과를 담은 2차원 배열 results가 매개변수로 주어질 때 정확하게 순위를 매길 수 있는 선수의 수를 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 선수의 수는 1명 이상 100명 이하입니다.
 - 경기 결과는 1개 이상 4,500개 이하입니다.
 - results 배열 각 행 [A, B]는 A 선수가 B 선수를 이겼다는 의미입니다.
 - 모든 경기 결과에는 모순이 없습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Node {
    public int index;
    List<Node> children;
    List<Node> parents;
    public Node(int _index) {
        index = _index;
        children = new List<Node>();
        parents = new List<Node>();
    }
    public void AddChild(Node _node) {
        if(!children.Contains(_node)) {
            children.Add(_node);
        }
    }
    public void AddParent(Node _node) {
        if(!parents.Contains(_node)) {
            parents.Add(_node);
        }
    }
    public void UseCheckChildren(bool[,] _used, int _index) {
        if(_used[_index,index]) {
            return;
        }
        if(index != _index) {
            _used[_index,index] = true;
        }
        for(int i = 0; i < children.Count; i++) {
            children[i].UseCheckChildren(_used, _index);
        }
    }
    public void UseCheckParents(bool[,] _used, int _index) {
        if(_used[_index,index]) {
            return;
        }
        if(index != _index) {
            _used[_index,index] = true;
        }
        for(int i = 0; i < parents.Count; i++) {
            parents[i].UseCheckParents(_used, _index);
        }
    }
}

public class Solution {
    public int solution(int n, int[,] results) {
        int answer = 0;
        bool[,] used = new bool[n,n];
        List<Node> list = new List<Node>();
        
        for(int i = 0; i < n; i++) {
            list.Add(new Node(i));
        }
        
        for(int i = 0; i < results.GetLength(0); i++) {
            int parent = results[i,0];
            int child = results[i,1];
            list[parent-1].AddChild(list[child-1]);
            list[child-1].AddParent(list[parent-1]);
        }
        
        for(int i = 0; i < list.Count; i++) {
            list[i].UseCheckChildren(used,list[i].index);
            list[i].UseCheckParents(used,list[i].index);
        }
        
        for(int i = 0; i < used.GetLength(0); i++) {
            int count = 0;
            for(int j = 0; j < used.GetLength(1); j++) {
                if(used[i,j]) {
                    count++;
                }
            }
            if(count == n - 1) {
                answer++;
            }
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.46ms, 31.4MB)
테스트 2 〉	통과 (1.33ms, 31.3MB)
테스트 3 〉	통과 (1.32ms, 31.2MB)
테스트 4 〉	통과 (1.93ms, 31.3MB)
테스트 5 〉	통과 (1.72ms, 31.1MB)
테스트 6 〉	통과 (1.50ms, 31.4MB)
테스트 7 〉	통과 (2.31ms, 31.3MB)
테스트 8 〉	통과 (5.54ms, 31.6MB)
테스트 9 〉	통과 (4.75ms, 31.8MB)
테스트 10 〉	통과 (5.35ms, 31.7MB)
```