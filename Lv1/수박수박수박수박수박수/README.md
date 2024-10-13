# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12922">수박수박수박수박수박수?</a>

### 문제설명

길이가 n이고, "수박수박수박수...."와 같은 패턴을 유지하는 문자열을 리턴하는 함수, solution을 완성하세요. 

예를들어 n이 4이면 "수박수박"을 리턴하고 3이라면 "수박수"를 리턴하면 됩니다.

***

### 제한사항

 - n은 길이 10,000이하인 자연수입니다.

***

### 답안
``` csharp
using System.Text;

public class Solution {
    public string solution(int n) {
        StringBuilder sb = new StringBuilder();

        for(int i = 0; i < n; i++) {
            if(i % 2 == 0) {
                sb.Append("수");
            }else{
                sb.Append("박");
            }
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.22ms, 31.1MB)
테스트 2 〉	통과 (0.24ms, 31.1MB)
테스트 3 〉	통과 (0.26ms, 31.2MB)
테스트 4 〉	통과 (0.27ms, 31MB)
테스트 5 〉	통과 (0.38ms, 31.1MB)
테스트 6 〉	통과 (0.22ms, 31MB)
테스트 7 〉	통과 (0.29ms, 30.7MB)
테스트 8 〉	통과 (0.21ms, 31.1MB)
테스트 9 〉	통과 (0.33ms, 31MB)
테스트 10 〉	통과 (0.21ms, 31MB)
테스트 11 〉	통과 (0.21ms, 31.2MB)
테스트 12 〉	통과 (0.24ms, 30.9MB)
테스트 13 〉	통과 (0.23ms, 31.1MB)
테스트 14 〉	통과 (0.30ms, 31.2MB)
테스트 15 〉	통과 (0.33ms, 31MB)
테스트 16 〉	통과 (0.20ms, 31.1MB)
```