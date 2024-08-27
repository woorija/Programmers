# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12909">올바른 괄호</a>

### 문제설명

괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어
 - "()()" 또는 "(())()" 는 올바른 괄호입니다.
 - ")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.
'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.

***

### 제한사항

 - 문자열 s의 길이 : 100,000 이하의 자연수
 - 문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public bool solution(string s) {
        bool answer;
        int count = 0;
        for(int i = 0; i < s.Length; i++) {
            if(s[i] == '(') {
                count++;
            }else{
                count--;
                if(count == -1) {
                    answer = false;
                    break;
                }
            }
        }
        if(count == 0) {
            answer = true;
        }else{
            answer = false;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.21ms, 31MB)
테스트 2 〉	통과 (0.27ms, 30.9MB)
테스트 3 〉	통과 (0.20ms, 31.2MB)
테스트 4 〉	통과 (0.26ms, 30.7MB)
테스트 5 〉	통과 (0.26ms, 31MB)
테스트 6 〉	통과 (0.22ms, 31MB)
테스트 7 〉	통과 (0.33ms, 31MB)
테스트 8 〉	통과 (0.21ms, 31.1MB)
테스트 9 〉	통과 (0.30ms, 31.2MB)
테스트 10 〉	통과 (0.22ms, 31MB)
테스트 11 〉	통과 (0.22ms, 31.2MB)
테스트 12 〉	통과 (0.22ms, 31MB)
테스트 13 〉	통과 (0.21ms, 31MB)
테스트 14 〉	통과 (0.20ms, 30.9MB)
테스트 15 〉	통과 (0.23ms, 30.7MB)
테스트 16 〉	통과 (0.19ms, 30.9MB)
테스트 17 〉	통과 (0.22ms, 30.9MB)
테스트 18 〉	통과 (0.22ms, 31MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (0.60ms, 31.2MB)
테스트 2 〉	통과 (0.64ms, 31.1MB)
```