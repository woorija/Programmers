# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/142085">디펜스 게임</a>

### 문제설명

준호는 요즘 디펜스 게임에 푹 빠져 있습니다. 디펜스 게임은 준호가 보유한 병사 n명으로 연속되는 적의 공격을 순서대로 막는 게임입니다. 디펜스 게임은 다음과 같은 규칙으로 진행됩니다.

 - 준호는 처음에 병사 n명을 가지고 있습니다.
 - 매 라운드마다 enemy[i]마리의 적이 등장합니다.
 - 남은 병사 중 enemy[i]명 만큼 소모하여 enemy[i]마리의 적을 막을 수 있습니다.
   - 예를 들어 남은 병사가 7명이고, 적의 수가 2마리인 경우, 현재 라운드를 막으면 7 - 2 = 5명의 병사가 남습니다.
   - 남은 병사의 수보다 현재 라운드의 적의 수가 더 많으면 게임이 종료됩니다.
 - 게임에는 무적권이라는 스킬이 있으며, 무적권을 사용하면 병사의 소모없이 한 라운드의 공격을 막을 수 있습니다.
 - 무적권은 최대 k번 사용할 수 있습니다.

준호는 무적권을 적절한 시기에 사용하여 최대한 많은 라운드를 진행하고 싶습니다.

준호가 처음 가지고 있는 병사의 수 n, 사용 가능한 무적권의 횟수 k, 매 라운드마다 공격해오는 적의 수가 순서대로 담긴 정수 배열 enemy가 매개변수로 주어집니다. 준호가 몇 라운드까지 막을 수 있는지 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ n ≤ 1,000,000,000
 - 1 ≤ k ≤ 500,000
 - 1 ≤ enemy의 길이 ≤ 1,000,000
 - 1 ≤ enemy[i] ≤ 1,000,000
 - enemy[i]에는 i + 1 라운드에서 공격해오는 적의 수가 담겨있습니다.
 - 모든 라운드를 막을 수 있는 경우에는 enemy[i]의 길이를 return 해주세요.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class MinHeap {
    private List<int> list;
    
    public MinHeap() {
        list = new List<int>();
    }
    
    public void Push(int _data) {
        list.Add(_data);
        int index = list.Count - 1;

        while(index > 0) {
            int parent = (index - 1) / 2;

            if(list[index] < list[parent]) {
                int temp = list[parent];
                list[parent] = list[index];
                list[index] = temp;
                index = parent;
            }else{
                break;
            }
        }
    }
    
    public int Pop() {
        int min = list[0];
        int lastIndex = list.Count - 1;
        list[0] = list[lastIndex];
        list.RemoveAt(lastIndex);
        lastIndex--;
        
        int parent = 0;
        
        while(parent * 2 + 1 <= lastIndex) {
            int child = parent * 2 + 1;

            if(child + 1 <= lastIndex && list[child] > list[child + 1]) {
                child++;
            }

            if(list[parent] > list[child]) {
                int temp = list[parent];
                list[parent] = list[child];
                list[child] = temp;
                parent = child;
            }else{
                break;
            }
        }
        return min;
    }
    
    public int Peek() {
        return list[0];
    }
}

public class Solution {
    public int solution(int n, int k, int[] enemy) {
        if(enemy.Length <= k) {
            return enemy.Length;
        }
        int answer = 0;
        MinHeap heap = new MinHeap();
        
        for(int i = 0; i < k; i++) {
            heap.Push(enemy[i]);
        }
        answer = k;
        
        for(int i = k; i < enemy.Length; i++) {
            if(enemy[i] > heap.Peek()) {
                n -= heap.Pop();
                heap.Push(enemy[i]);
            }else{
                n -= enemy[i];
            }
            
            if(n < 0) {
                break;
            }
            answer++;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.11ms, 31MB)
테스트 2 〉	통과 (1.81ms, 32.8MB)
테스트 3 〉	통과 (73.59ms, 51.3MB)
테스트 4 〉	통과 (9.63ms, 50.4MB)
테스트 5 〉	통과 (0.25ms, 31.2MB)
테스트 6 〉	통과 (56.00ms, 53MB)
테스트 7 〉	통과 (26.73ms, 50.3MB)
테스트 8 〉	통과 (5.21ms, 50MB)
테스트 9 〉	통과 (22.00ms, 50.4MB)
테스트 10 〉	통과 (32.81ms, 50.3MB)
테스트 11 〉	통과 (0.97ms, 49.9MB)
테스트 12 〉	통과 (1.08ms, 49.9MB)
테스트 13 〉	통과 (0.33ms, 31.2MB)
테스트 14 〉	통과 (0.27ms, 31.3MB)
테스트 15 〉	통과 (0.73ms, 31.1MB)
테스트 16 〉	통과 (0.99ms, 31.2MB)
테스트 17 〉	통과 (0.31ms, 31.5MB)
테스트 18 〉	통과 (0.28ms, 31.2MB)
테스트 19 〉	통과 (0.95ms, 31.3MB)
테스트 20 〉	통과 (0.71ms, 31.3MB)
테스트 21 〉	통과 (1.01ms, 31.2MB)
테스트 22 〉	통과 (0.27ms, 31.2MB)
테스트 23 〉	통과 (0.97ms, 31MB)
테스트 24 〉	통과 (0.96ms, 31.4MB)
테스트 25 〉	통과 (0.96ms, 30.9MB)
테스트 26 〉	통과 (0.99ms, 31.2MB)
테스트 27 〉	통과 (0.94ms, 31.1MB)
테스트 28 〉	통과 (0.68ms, 31.1MB)
테스트 29 〉	통과 (0.96ms, 31.4MB)
테스트 30 〉	통과 (0.95ms, 31.3MB)
테스트 31 〉	통과 (0.96ms, 31.4MB)
```