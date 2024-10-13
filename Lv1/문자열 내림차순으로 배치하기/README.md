# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12917">문자열 내림차순으로 배치하기
</a>

### 문제설명

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.

s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

***

### 제한사항

 - str은 길이 1 이상인 문자열입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public string solution(string s) {
        char[] arr = s.ToCharArray();
        Array.Sort(arr);
        Array.Reverse(arr);
        string answer = new string(arr);
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.84ms, 31.1MB)
테스트 2 〉	통과 (1.87ms, 30.9MB)
테스트 3 〉	통과 (1.81ms, 31.2MB)
테스트 4 〉	통과 (1.82ms, 30.9MB)
테스트 5 〉	통과 (1.82ms, 31.1MB)
테스트 6 〉	통과 (1.82ms, 30.9MB)
테스트 7 〉	통과 (1.88ms, 31.1MB)
테스트 8 〉	통과 (1.84ms, 31MB)
테스트 9 〉	통과 (1.80ms, 31.2MB)
테스트 10 〉	통과 (1.85ms, 30.9MB)
테스트 11 〉	통과 (2.08ms, 31.3MB)
테스트 12 〉	통과 (1.80ms, 31.1MB)
테스트 13 〉	통과 (1.79ms, 31.1MB)
테스트 14 〉	통과 (1.83ms, 31.3MB)
테스트 15 〉	통과 (1.61ms, 31.3MB)
테스트 16 〉	통과 (1.60ms, 31MB)
```