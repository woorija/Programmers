# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/92343">양과 늑대</a>

### 문제설명

2진 트리 모양 초원의 각 노드에 늑대와 양이 한 마리씩 놓여 있습니다. 이 초원의 루트 노드에서 출발하여 각 노드를 돌아다니며 양을 모으려 합니다. 각 노드를 방문할 때 마다 해당 노드에 있던 양과 늑대가 당신을 따라오게 됩니다. 이때, 늑대는 양을 잡아먹을 기회를 노리고 있으며, 당신이 모은 양의 수보다 늑대의 수가 같거나 더 많아지면 바로 모든 양을 잡아먹어 버립니다. 당신은 중간에 양이 늑대에게 잡아먹히지 않도록 하면서 최대한 많은 수의 양을 모아서 다시 루트 노드로 돌아오려 합니다.

각 노드에 있는 양 또는 늑대에 대한 정보가 담긴 배열 info, 2진 트리의 각 노드들의 연결 관계를 담은 2차원 배열 edges가 매개변수로 주어질 때, 문제에 제시된 조건에 따라 각 노드를 방문하면서 모을 수 있는 양은 최대 몇 마리인지 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 2 ≤ info의 길이 ≤ 17
   - info의 원소는 0 또는 1 입니다.
   - info[i]는 i번 노드에 있는 양 또는 늑대를 나타냅니다.
   - 0은 양, 1은 늑대를 의미합니다.
   - info[0]의 값은 항상 0입니다. 즉, 0번 노드(루트 노드)에는 항상 양이 있습니다.
 - edges의 세로(행) 길이 = info의 길이 - 1
   - edges의 가로(열) 길이 = 2
   - edges의 각 행은 [부모 노드 번호, 자식 노드 번호] 형태로, 서로 연결된 두 노드를 나타냅니다.
   - 동일한 간선에 대한 정보가 중복해서 주어지지 않습니다.
   - 항상 하나의 이진 트리 형태로 입력이 주어지며, 잘못된 데이터가 주어지는 경우는 없습니다.
   - 0번 노드는 항상 루트 노드입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Node {
    public int index;
    public Node parent;
    public int sheep;
    
    public Node(int _index, int _sheep) {
        index = _index;
        parent = null;
        sheep = _sheep;
    }
    
    public void SetParent(Node _other) {
        parent = _other;
    }
    
    public bool GetWolf() {
        bool flag = sheep == 0 ? false : true;
        if(parent == null) {
            return flag;
        }
        if(!flag) {
            flag = parent.GetWolf();
        }
        return flag; 
    }
}
public class Solution {
    int answer;
    List<Node> list;
    Dictionary<int, List<int>> graph;
    
    public int solution(int[] info, int[,] edges) {
        list = new List<Node>();
        List<Node> sheepList = new List<Node>();
        graph = new Dictionary<int, List<int>>();
        List<int> baseList = new List<int>();
        
        for(int i = 0; i < info.Length; i++) {
            Node temp = new Node(i,info[i]);
            list.Add(temp);
            if(info[i] == 0) {
                sheepList.Add(temp);
            }
            graph[i] = new List<int>();
        }
        
        for(int i = 0; i < edges.GetLength(0); i++) {
            list[edges[i,1]].SetParent(list[edges[i,0]]);
            graph[edges[i,0]].Add(edges[i,1]);
        }
        
        for(int i = sheepList.Count - 1; i >= 0; i--) {
            if(sheepList[i].GetWolf()) {
                sheepList.RemoveAt(i);
            }
        }
        
        for(int i = 0; i < sheepList.Count; i++) {
            baseList.Add(sheepList[i].index);
        }
        
        
        int count = baseList.Count;
        answer = count;
        for(int i = 0; i < count; i++) {
            for(int j = 0; j < graph[baseList[i]].Count; j++) {
                if(!baseList.Contains(graph[baseList[i]][j])) {
                    baseList.Add(graph[baseList[i]][j]);
                }
            }
        }
        
        baseList.RemoveRange(0,count);
        
        for(int i = 0; i < baseList.Count; i++) {
            dfs(baseList[i], count, 0, baseList);
        }
        
        return answer;
    }
    
    void dfs(int _index, int _sheep, int _wolf, List<int> _list) {
        int sheep = _sheep;
        int wolf = _wolf;
        if(list[_index].sheep == 0) {
            sheep++;
            answer = Math.Max(answer, sheep);
        }else{
            wolf++;
        }
        if(sheep <= wolf) {
            return;
        }
        
        List<int> copyList = _list.ConvertAll(x => x);
        
        for(int i = 0; i < graph[_index].Count; i++) {
            copyList.Add(graph[_index][i]);
        }
        copyList.Remove(_index);
        
        for(int i = 0; i < copyList.Count; i++) {
            dfs(copyList[i], sheep, wolf, copyList);
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.20ms, 30.7MB)
테스트 2 〉	통과 (3.88ms, 31.2MB)
테스트 3 〉	통과 (3.73ms, 31.1MB)
테스트 4 〉	통과 (3.00ms, 30.9MB)
테스트 5 〉	통과 (4.03ms, 31.4MB)
테스트 6 〉	통과 (3.68ms, 31.2MB)
테스트 7 〉	통과 (3.66ms, 31.1MB)
테스트 8 〉	통과 (3.92ms, 31.3MB)
테스트 9 〉	통과 (4.04ms, 31MB)
테스트 10 〉	통과 (3.69ms, 31.2MB)
테스트 11 〉	통과 (5.58ms, 31.1MB)
테스트 12 〉	통과 (4.00ms, 31.3MB)
테스트 13 〉	통과 (3.70ms, 31.3MB)
테스트 14 〉	통과 (3.72ms, 31MB)
테스트 15 〉	통과 (3.79ms, 31.1MB)
테스트 16 〉	통과 (3.99ms, 31MB)
테스트 17 〉	통과 (3.85ms, 30.9MB)
테스트 18 〉	통과 (3.71ms, 31.2MB)
```