# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42860">조이스틱</a>

### 문제설명

조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.

ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA

조이스틱을 각 방향으로 움직이면 아래와 같습니다.

```
 ▲ - 다음 알파벳
 ▼ - 이전 알파벳 (A에서 아래쪽으로 이동하면 Z로)
 ◀ - 커서를 왼쪽으로 이동 (첫 번째 위치에서 왼쪽으로 이동하면 마지막 문자에 커서)
 ▶ - 커서를 오른쪽으로 이동 (마지막 위치에서 오른쪽으로 이동하면 첫 번째 문자에 커서)
```

예를 들어 아래의 방법으로 "JAZ"를 만들 수 있습니다.

```
 - 첫 번째 위치에서 조이스틱을 위로 9번 조작하여 J를 완성합니다.
 - 조이스틱을 왼쪽으로 1번 조작하여 커서를 마지막 문자 위치로 이동시킵니다.
 - 마지막 위치에서 조이스틱을 아래로 1번 조작하여 Z를 완성합니다.
 따라서 11번 이동시켜 "JAZ"를 만들 수 있고, 이때가 최소 이동입니다.
```

만들고자 하는 이름 name이 매개변수로 주어질 때, 이름에 대해 조이스틱 조작 횟수의 최솟값을 return 하도록 solution 함수를 만드세요.

***

### 제한사항

 - name은 알파벳 대문자로만 이루어져 있습니다.
 - name의 길이는 1 이상 20 이하입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(string name) {
        if(name.Replace("A", "") == "") {
            return 0;
        }
        
        int answer = 0;
        int length = name.Length;
        int changeCount = 0;
        int moveCount = name.Length - 1;
        List<int> notA = new List<int>();
        
        for(int i = 0; i < length; i++) {
            if(name[i] <= 'N') {
                changeCount += name[i] - 'A';
            }else{
                changeCount += 26 - (name[i] - 'A');
            }
            
            if(i != 0 && name[i] != 'A') {
                notA.Add(i);
            }
        }
        
        moveCount = Math.Min(moveCount, notA[notA.Count - 1]);
        moveCount = Math.Min(moveCount, name.Length - notA[0]);
        
        for(int i = 0; i < notA.Count - 1; i++) {
            int temp = notA[i];
            moveCount = Math.Min(moveCount, temp * 2 + (length - notA[i + 1]));
        }
        
        for(int i = notA.Count - 1; i > 0; i--) {
            int temp = length - notA[i];
            moveCount = Math.Min(moveCount, temp * 2 + notA[i - 1]);
        }
        
        return changeCount + moveCount;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.81ms, 31.1MB)
테스트 2 〉	통과 (0.90ms, 31.4MB)
테스트 3 〉	통과 (1.46ms, 31.3MB)
테스트 4 〉	통과 (1.14ms, 31.1MB)
테스트 5 〉	통과 (1.47ms, 31.4MB)
테스트 6 〉	통과 (1.18ms, 31.3MB)
테스트 7 〉	통과 (0.93ms, 31.1MB)
테스트 8 〉	통과 (0.91ms, 31.3MB)
테스트 9 〉	통과 (0.72ms, 31.2MB)
테스트 10 〉	통과 (0.91ms, 30.9MB)
테스트 11 〉	통과 (1.09ms, 31.5MB)
테스트 12 〉	통과 (0.90ms, 31.5MB)
테스트 13 〉	통과 (0.99ms, 31.2MB)
테스트 14 〉	통과 (0.91ms, 31.2MB)
테스트 15 〉	통과 (0.93ms, 31.4MB)
테스트 16 〉	통과 (0.70ms, 31.2MB)
테스트 17 〉	통과 (0.70ms, 31MB)
테스트 18 〉	통과 (0.96ms, 31.2MB)
테스트 19 〉	통과 (0.96ms, 31.1MB)
테스트 20 〉	통과 (0.94ms, 31.2MB)
테스트 21 〉	통과 (0.97ms, 31.3MB)
테스트 22 〉	통과 (0.98ms, 31.3MB)
테스트 23 〉	통과 (0.97ms, 31.1MB)
테스트 24 〉	통과 (0.91ms, 30.8MB)
테스트 25 〉	통과 (0.92ms, 31.4MB)
테스트 26 〉	통과 (0.94ms, 31.2MB)
테스트 27 〉	통과 (0.94ms, 31MB)
```