# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12951">JadenCase 문자열 만들기</a>

### 문제설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다.
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

***

### 제한사항

 - s는 길이 1 이상 200 이하인 문자열입니다.
 - s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
   - 숫자는 단어의 첫 문자로만 나옵니다.
   - 숫자로만 이루어진 단어는 없습니다.
   - 공백문자가 연속해서 나올 수 있습니다.

***

### 답안
``` csharp
using System;
public class Solution {
    public string solution(string s) {
        string answer = "";
        if(Char.IsLower(s[0])) {
            answer += Char.ToUpper(s[0]);
        }else{
            answer += s[0];
        }
        
        for(int i = 1; i < s.Length; i++) {
            if(s[i-1] == ' '){
                if(Char.IsLower(s[i])) {
                    answer += Char.ToUpper(s[i]);
                }else{
                    answer += s[i];
                }
            }else{
                if(Char.IsUpper(s[i])) {
                    answer += Char.ToLower(s[i]);
                }else{
                    answer += s[i];
                }
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.69ms, 31.2MB)
테스트 2 〉	통과 (0.73ms, 31.1MB)
테스트 3 〉	통과 (0.75ms, 31.1MB)
테스트 4 〉	통과 (0.69ms, 31.1MB)
테스트 5 〉	통과 (0.75ms, 31.1MB)
테스트 6 〉	통과 (0.72ms, 31.4MB)
테스트 7 〉	통과 (0.70ms, 31.2MB)
테스트 8 〉	통과 (0.69ms, 31.4MB)
테스트 9 〉	통과 (0.68ms, 31.1MB)
테스트 10 〉	통과 (0.73ms, 31MB)
테스트 11 〉	통과 (0.72ms, 31.1MB)
테스트 12 〉	통과 (0.70ms, 31.1MB)
테스트 13 〉	통과 (0.66ms, 31.2MB)
테스트 14 〉	통과 (0.67ms, 31.4MB)
테스트 15 〉	통과 (0.73ms, 31.4MB)
테스트 16 〉	통과 (0.71ms, 31.1MB)
테스트 17 〉	통과 (0.64ms, 30.8MB)
테스트 18 〉	통과 (0.68ms, 30.9MB)
```