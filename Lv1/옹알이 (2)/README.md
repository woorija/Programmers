# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/133499">옹알이 (2)</a>

### 문제설명

머쓱이는 태어난 지 11개월 된 조카를 돌보고 있습니다. 조카는 아직 "aya", "ye", "woo", "ma" 네 가지 발음과 네 가지 발음을 조합해서 만들 수 있는 발음밖에 하지 못하고 연속해서 같은 발음을 하는 것을 어려워합니다. 문자열 배열 babbling이 매개변수로 주어질 때, 머쓱이의 조카가 발음할 수 있는 단어의 개수를 return하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ babbling의 길이 ≤ 100
 - 1 ≤ babbling[i]의 길이 ≤ 30
 - 문자열은 알파벳 소문자로만 이루어져 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string[] babbling) {
        int answer = 0;
        for(int i = 0; i < babbling.Length; i++) {
            string str = babbling[i].Replace("aya", "1").Replace("ye", "2").Replace("woo", "3").Replace("ma", "4");
            bool check = true;
            if(int.TryParse(str, out int result)) {
                for(int j = 0; j < str.Length - 1; j++) {
                    if(str[j] == str[j + 1]) {
                        check = false;
                        break;
                    }
                }
            }else{
                check = false;
            }
            if(check) {
                answer++;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.97ms, 31.6MB)
테스트 2 〉	통과 (0.96ms, 31.1MB)
테스트 3 〉	통과 (1.49ms, 31.5MB)
테스트 4 〉	통과 (1.03ms, 31.6MB)
테스트 5 〉	통과 (1.43ms, 31.6MB)
테스트 6 〉	통과 (1.01ms, 31.4MB)
테스트 7 〉	통과 (1.00ms, 31.7MB)
테스트 8 〉	통과 (1.48ms, 31.1MB)
테스트 9 〉	통과 (0.97ms, 31.6MB)
테스트 10 〉	통과 (0.96ms, 31MB)
테스트 11 〉	통과 (0.98ms, 31.4MB)
테스트 12 〉	통과 (1.06ms, 31.7MB)
테스트 13 〉	통과 (1.06ms, 31.4MB)
테스트 14 〉	통과 (1.06ms, 31.7MB)
테스트 15 〉	통과 (1.10ms, 31.3MB)
테스트 16 〉	통과 (1.04ms, 31.4MB)
테스트 17 〉	통과 (1.06ms, 31.1MB)
테스트 18 〉	통과 (1.12ms, 31.2MB)
테스트 19 〉	통과 (1.10ms, 31.2MB)
테스트 20 〉	통과 (0.98ms, 31.5MB)
```