# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12948">핸드폰 번호 가리기</a>

### 문제설명

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.

전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

***

### 제한사항

 - phone_number는 길이 4 이상, 20이하인 문자열입니다.

***

### 답안
``` csharp
public class Solution {
    public string solution(string phone_number) {
        string answer = "";
        for(int i = 0; i < phone_number.Length - 4; i++) {
            answer += "*";
        }
        for(int i = phone_number.Length - 4; i < phone_number.Length; i++) {
            answer += phone_number[i];
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.29ms, 31.1MB)
테스트 2 〉	통과 (0.27ms, 30.9MB)
테스트 3 〉	통과 (0.26ms, 31.1MB)
테스트 4 〉	통과 (0.27ms, 31.2MB)
테스트 5 〉	통과 (0.27ms, 31.3MB)
테스트 6 〉	통과 (0.30ms, 31.1MB)
테스트 7 〉	통과 (0.28ms, 30.4MB)
테스트 8 〉	통과 (0.28ms, 30.5MB)
테스트 9 〉	통과 (0.26ms, 31.2MB)
테스트 10 〉	통과 (0.28ms, 31.2MB)
테스트 11 〉	통과 (0.28ms, 30.7MB)
```