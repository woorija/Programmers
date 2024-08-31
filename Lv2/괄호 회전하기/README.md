# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/76502">괄호 회전하기</a>

### 문제설명

다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.

 - (), [], {} 는 모두 올바른 괄호 문자열입니다.
 - 만약 A가 올바른 괄호 문자열이라면, (A), [A], {A} 도 올바른 괄호 문자열입니다. 예를 들어, [] 가 올바른 괄호 문자열이므로, ([]) 도 올바른 괄호 문자열입니다.
 - 만약 A, B가 올바른 괄호 문자열이라면, AB 도 올바른 괄호 문자열입니다. 예를 들어, {} 와 ([]) 가 올바른 괄호 문자열이므로, {}([]) 도 올바른 괄호 문자열입니다.
대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 s가 매개변수로 주어집니다. 이 s를 왼쪽으로 x (0 ≤ x < (s의 길이)) 칸만큼 회전시켰을 때 s가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - s의 길이는 1 이상 1,000 이하입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string s) {
        if(s.Length % 2 != 0) {
            return 0;
        }
        int answer = 0;
        string str = s;
        string temp = s;
        for(int i = 0; i < s.Length; i++) {
            str = s.Substring(i) + s.Substring(0, i);
            while(true) {
                temp = str.Replace("()","").Replace("{}","").Replace("[]","");
                if(temp == "") {
                    answer++;
                    break;
                }else if(temp == str) {
                    break;
                }
                str = temp;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (679.42ms, 34.6MB)
테스트 2 〉	통과 (133.85ms, 34.8MB)
테스트 3 〉	통과 (80.16ms, 34.9MB)
테스트 4 〉	통과 (61.67ms, 34.6MB)
테스트 5 〉	통과 (51.55ms, 34.8MB)
테스트 6 〉	통과 (112.89ms, 34.8MB)
테스트 7 〉	통과 (84.40ms, 34.9MB)
테스트 8 〉	통과 (68.33ms, 34.9MB)
테스트 9 〉	통과 (54.73ms, 34.9MB)
테스트 10 〉	통과 (47.36ms, 34.7MB)
테스트 11 〉	통과 (38.01ms, 34.8MB)
테스트 12 〉	통과 (0.28ms, 31.4MB)
테스트 13 〉	통과 (0.28ms, 31.3MB)
테스트 14 〉	통과 (0.32ms, 31MB)
```