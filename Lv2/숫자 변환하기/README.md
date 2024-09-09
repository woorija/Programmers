# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/154538">숫자 변환하기</a>

### 문제설명

자연수 x를 y로 변환하려고 합니다. 사용할 수 있는 연산은 다음과 같습니다.

 - x에 n을 더합니다
 - x에 2를 곱합니다.
 - x에 3을 곱합니다.

자연수 x, y, n이 매개변수로 주어질 때, x를 y로 변환하기 위해 필요한 최소 연산 횟수를 return하도록 solution 함수를 완성해주세요. 이때 x를 y로 만들 수 없다면 -1을 return 해주세요.

***

### 제한사항

 - 1 ≤ x ≤ y ≤ 1,000,000
 - 1 ≤ n < y

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Counter{
    public int num;
    public int count;
    public Counter(int _num, int _count){
        num = _num;
        count = _count;
    }
}
public class Solution {
    public int solution(int x, int y, int n) {
        int answer = 0;
        if(x != y) {
            answer = bfs(x, y, n);
        }
        return answer;
    }
    public int bfs(int x, int y, int n){
        Queue<Counter> queue = new Queue<Counter>();
        HashSet<int> check = new HashSet<int>();
        queue.Enqueue(new Counter(x, 0));
        while(queue.Count != 0){
            Counter counter = queue.Dequeue();
            int num = counter.num;
            int count = counter.count;
            if(check.Contains(num)) {
                continue;
            }
            check.Add(num);
            if(num == y) {
                return count;
            }
            if(num * 3 <= y){
                queue.Enqueue(new Counter(num * 3, count + 1));
            }
            if(num * 2 <= y){
                queue.Enqueue(new Counter(num * 2, count + 1));
            }
            if(num + n <= y){
                queue.Enqueue(new Counter(num + n, count + 1));
            }
        }
        return -1;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.86ms, 31.2MB)
테스트 2 〉	통과 (1.35ms, 30.9MB)
테스트 3 〉	통과 (2.09ms, 31.4MB)
테스트 4 〉	통과 (2.06ms, 31.1MB)
테스트 5 〉	통과 (28.27ms, 41.4MB)
테스트 6 〉	통과 (0.17ms, 31.3MB)
테스트 7 〉	통과 (19.42ms, 41.6MB)
테스트 8 〉	통과 (2.35ms, 31MB)
테스트 9 〉	통과 (135.71ms, 70.5MB)
테스트 10 〉	통과 (120.00ms, 73.4MB)
테스트 11 〉	통과 (54.83ms, 45.5MB)
테스트 12 〉	통과 (2.14ms, 31.2MB)
테스트 13 〉	통과 (1.36ms, 30.8MB)
테스트 14 〉	통과 (2.69ms, 31.5MB)
테스트 15 〉	통과 (1.82ms, 31.1MB)
테스트 16 〉	통과 (2.92ms, 31.5MB)
```