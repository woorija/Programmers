# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/155652">둘만의 암호</a>

### 문제설명

두 문자열 s와 skip, 그리고 자연수 index가 주어질 때, 다음 규칙에 따라 문자열을 만들려 합니다. 암호의 규칙은 다음과 같습니다.

 - 문자열 s의 각 알파벳을 index만큼 뒤의 알파벳으로 바꿔줍니다.
 - index만큼의 뒤의 알파벳이 z를 넘어갈 경우 다시 a로 돌아갑니다.
 - skip에 있는 알파벳은 제외하고 건너뜁니다.

예를 들어 s = "aukks", skip = "wbqd", index = 5일 때, a에서 5만큼 뒤에 있는 알파벳은 f지만 [b, c, d, e, f]에서 'b'와 'd'는 skip에 포함되므로 세지 않습니다. 따라서 'b', 'd'를 제외하고 'a'에서 5만큼 뒤에 있는 알파벳은 [c, e, f, g, h] 순서에 의해 'h'가 됩니다. 나머지 "ukks" 또한 위 규칙대로 바꾸면 "appy"가 되며 결과는 "happy"가 됩니다.

두 문자열 s와 skip, 그리고 자연수 index가 매개변수로 주어질 때 위 규칙대로 s를 변환한 결과를 return하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 5 ≤ s의 길이 ≤ 50
 - 1 ≤ skip의 길이 ≤ 10
 - s와 skip은 알파벳 소문자로만 이루어져 있습니다.
   - skip에 포함되는 알파벳은 s에 포함되지 않습니다.
 - 1 ≤ index ≤ 20

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public string solution(string s, string skip, int index) {
        char[] arr = s.ToCharArray();
        List<char> list = new List<char>(26 - skip.Length);
        List<char> skips = new List<char>(skip.Length);
        for(int i = 0; i < skip.Length; i++) {
            skips.Add(skip[i]);
        }
        for(int i = 0; i < 26; i++) {
            char temp = (char)(i + 'a');
            if(!skips.Contains(temp)) {
                list.Add(temp);
            }
        }
        for(int i = 0; i < arr.Length; i++) {
            int arrIndex = list.IndexOf(arr[i]);
            arrIndex = (arrIndex + index) % list.Count;
            arr[i] = list[arrIndex];
        }
        return new string(arr);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.32ms, 31.2MB)
테스트 2 〉	통과 (1.37ms, 31.2MB)
테스트 3 〉	통과 (1.32ms, 30.9MB)
테스트 4 〉	통과 (1.39ms, 31.1MB)
테스트 5 〉	통과 (1.53ms, 31.1MB)
테스트 6 〉	통과 (1.49ms, 31.3MB)
테스트 7 〉	통과 (1.31ms, 31.1MB)
테스트 8 〉	통과 (1.44ms, 30.9MB)
테스트 9 〉	통과 (1.31ms, 30.9MB)
테스트 10 〉	통과 (1.28ms, 31.3MB)
테스트 11 〉	통과 (1.52ms, 30.8MB)
테스트 12 〉	통과 (1.39ms, 31.5MB)
테스트 13 〉	통과 (2.02ms, 31.3MB)
테스트 14 〉	통과 (1.34ms, 31.2MB)
테스트 15 〉	통과 (1.31ms, 31.1MB)
테스트 16 〉	통과 (1.38ms, 31.2MB)
테스트 17 〉	통과 (1.42ms, 31MB)
테스트 18 〉	통과 (1.47ms, 31.1MB)
테스트 19 〉	통과 (2.12ms, 31.1MB)
```