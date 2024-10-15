# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12930">이상한 문자 만들기</a>

### 문제설명

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

***

### 제한사항

 - 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
 - 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.

***

### 답안
``` csharp
using System.Text;

public class Solution {
    public string solution(string s) {
        StringBuilder sb = new StringBuilder();
        int count = 0;
        for(int i = 0; i < s.Length; i++) {
            if(count % 2 == 0) {
                if('a' <= s[i] && s[i] <= 'z') {
                    sb.Append((char)(s[i] - 32));
                }else{
                    sb.Append(s[i]);
                }
            }else{
                if('A' <= s[i] && s[i] <= 'Z') {
                    sb.Append((char)(s[i] + 32));
                }else{
                    sb.Append(s[i]);
                }
            }
            if(s[i] == ' ') {
                count = -1;
            }
            count++;
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.58ms, 31.2MB)
테스트 2 〉	통과 (0.47ms, 31.3MB)
테스트 3 〉	통과 (0.52ms, 31.2MB)
테스트 4 〉	통과 (0.32ms, 31MB)
테스트 5 〉	통과 (0.41ms, 31.1MB)
테스트 6 〉	통과 (0.32ms, 31MB)
테스트 7 〉	통과 (0.30ms, 31.3MB)
테스트 8 〉	통과 (0.31ms, 31.2MB)
테스트 9 〉	통과 (0.30ms, 30.9MB)
테스트 10 〉	통과 (0.30ms, 31.1MB)
테스트 11 〉	통과 (0.30ms, 31.1MB)
테스트 12 〉	통과 (0.34ms, 30.9MB)
테스트 13 〉	통과 (0.32ms, 31.3MB)
테스트 14 〉	통과 (0.31ms, 31.3MB)
테스트 15 〉	통과 (0.29ms, 30.9MB)
테스트 16 〉	통과 (0.30ms, 31.1MB)
```