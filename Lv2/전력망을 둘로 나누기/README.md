# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/86971">전력망을 둘로 나누기</a>

### 문제설명

n개의 송전탑이 전선을 통해 하나의 트리 형태로 연결되어 있습니다. 당신은 이 전선들 중 하나를 끊어서 현재의 전력망 네트워크를 2개로 분할하려고 합니다. 이때, 두 전력망이 갖게 되는 송전탑의 개수를 최대한 비슷하게 맞추고자 합니다.

송전탑의 개수 n, 그리고 전선 정보 wires가 매개변수로 주어집니다. 전선들 중 하나를 끊어서 송전탑 개수가 가능한 비슷하도록 두 전력망으로 나누었을 때, 두 전력망이 가지고 있는 송전탑 개수의 차이(절대값)를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - n은 2 이상 100 이하인 자연수입니다.
 - wires는 길이가 n-1인 정수형 2차원 배열입니다.
   - wires의 각 원소는 [v1, v2] 2개의 자연수로 이루어져 있으며, 이는 전력망의 v1번 송전탑과 v2번 송전탑이 전선으로 연결되어 있다는 것을 의미합니다.
   - 1 ≤ v1 < v2 ≤ n 입니다.
   - 전력망 네트워크가 하나의 트리 형태가 아닌 경우는 입력으로 주어지지 않습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Node {
    public int count;
    public List<Node> children;

    public Node() {
        count = 1;
        children = new List<Node>();
    }
    public int GetCount() {
        count = 1;
        for(int i = 0; i < children.Count; i++) {
            count += children[i].GetCount();
        }
        return count;
    }
    public void AddChild(Node _node) {
        children.Add(_node);
    }
}

public class Solution {
    public int solution(int n, int[,] wires) {
        int answer = 101;
        List<Node> nodeList = new List<Node>();
        int[] counts = new int[n];
        bool[] visit = new bool[n];
        int current;
        HashSet<int> used = new HashSet<int>();
        Queue<int> nextNodes = new Queue<int>();
        List<int> roots = new List<int>();
        
        for(int i = 0; i < n; i++) {
            nodeList.Add(new Node());
        }
        for(int i = 0; i < wires.GetLength(0); i++) {
            if(!roots.Contains(wires[i,0])) {
                roots.Add(wires[i,0]);
            }
        }
        for(int i = 0; i < wires.GetLength(0); i++) {
            roots.Remove(wires[i,1]);
        }
        
        current = roots[0] - 1;
        used.Add(current);
        for(int i = 0; i < n; i++) {
            for(int j = 0; j < wires.GetLength(0); j++) {
                if(visit[j]) continue;
                int check = -1;
                if(wires[j,0] == current + 1) {
                    if(!used.Contains(wires[j,1] - 1)) {
                        nodeList[current].AddChild(nodeList[wires[j,1] - 1]);
                        check = 1;
                    }
                }else if(wires[j,1] == current + 1) {
                    if(!used.Contains(wires[j,0] - 1)) {
                        nodeList[current].AddChild(nodeList[wires[j,0] - 1]);
                        check = 0;
                    }
                }
                if(check != -1) {
                    nextNodes.Enqueue(wires[j,check] - 1);
                    visit[j] = true;
                }
            }
            
            if(nextNodes.Count != 0) {
                current = nextNodes.Dequeue();
                used.Add(current);
            }
        }
        for(int i = 0; i < n; i++) {
            int temp1 = nodeList[i].GetCount();
            int temp2 = n - temp1;
            answer = Math.Min(answer, Math.Abs(temp2 - temp1));
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.08ms, 31.4MB)
테스트 2 〉	통과 (3.22ms, 31.2MB)
테스트 3 〉	통과 (3.15ms, 31.3MB)
테스트 4 〉	통과 (3.13ms, 31.2MB)
테스트 5 〉	통과 (3.16ms, 31.3MB)
테스트 6 〉	통과 (3.08ms, 31.1MB)
테스트 7 〉	통과 (2.97ms, 31.3MB)
테스트 8 〉	통과 (3.03ms, 31.1MB)
테스트 9 〉	통과 (3.15ms, 31.2MB)
테스트 10 〉	통과 (3.15ms, 30.9MB)
테스트 11 〉	통과 (3.18ms, 31.1MB)
테스트 12 〉	통과 (3.32ms, 31.4MB)
테스트 13 〉	통과 (3.15ms, 31.2MB)
```