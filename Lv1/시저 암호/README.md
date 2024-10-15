# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12926">시저 암호</a>

### 문제설명

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

***

### 제한사항

 - 공백은 아무리 밀어도 공백입니다.
 - s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
 - s의 길이는 8000이하입니다.
 - n은 1 이상, 25이하인 자연수입니다.

***

### 답안
``` csharp
using System.Text;

public class Solution {
    public string solution(string s, int n) {
        StringBuilder sb = new StringBuilder();
        int length = s.Length;
        for(int i = 0; i < length; i++) {
            if('A' <= s[i] && s[i] <= 'Z') {
                int temp = s[i] - 'A';
                temp = (temp + n) % 26;
                sb.Append((char)(temp + 'A'));
            }else if('a' <= s[i] && s[i] <= 'z') {
                int temp = s[i] - 'a';
                temp = (temp + n) % 26;
                sb.Append((char)(temp + 'a'));
            }else{
                sb.Append(s[i]);
            }
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.29ms, 30.8MB)
테스트 2 〉	통과 (0.30ms, 31.1MB)
테스트 3 〉	통과 (0.30ms, 30.8MB)
테스트 4 〉	통과 (0.28ms, 30.9MB)
테스트 5 〉	통과 (0.27ms, 31.1MB)
테스트 6 〉	통과 (0.28ms, 30.9MB)
테스트 7 〉	통과 (0.30ms, 31.1MB)
테스트 8 〉	통과 (0.33ms, 30.8MB)
테스트 9 〉	통과 (0.31ms, 30.8MB)
테스트 10 〉	통과 (0.29ms, 31.2MB)
테스트 11 〉	통과 (0.30ms, 31.1MB)
테스트 12 〉	통과 (0.30ms, 31.2MB)
테스트 13 〉	통과 (0.44ms, 30.7MB)
```