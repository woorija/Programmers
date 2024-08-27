# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/70129">이진 변환 반복하기</a>

### 문제설명

0과 1로 이루어진 어떤 문자열 x에 대한 이진 변환을 다음과 같이 정의합니다.

x의 모든 0을 제거합니다.
x의 길이를 c라고 하면, x를 "c를 2진법으로 표현한 문자열"로 바꿉니다.
예를 들어, x = "0111010"이라면, x에 이진 변환을 가하면 x = "0111010" -> "1111" -> "100" 이 됩니다.

0과 1로 이루어진 문자열 s가 매개변수로 주어집니다. s가 "1"이 될 때까지 계속해서 s에 이진 변환을 가했을 때, 이진 변환의 횟수와 변환 과정에서 제거된 모든 0의 개수를 각각 배열에 담아 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - s의 길이는 1 이상 150,000 이하입니다.
 - s에는 '1'이 최소 하나 이상 포함되어 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(string s) {
        int count = 0;
        int delete = 0;
        string temp = s;
        while(temp != "1"){
            count++;
            delete += temp.Length;
            temp = temp.Replace("0", string.Empty);
            delete -= temp.Length;
            temp = Convert.ToString(temp.Length,2);
        }
        int[] answer = new int[] { count, delete };
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.60ms, 31.5MB)
테스트 2 〉	통과 (8.36ms, 33.6MB)
테스트 3 〉	통과 (0.65ms, 31.4MB)
테스트 4 〉	통과 (0.84ms, 31.2MB)
테스트 5 〉	통과 (0.63ms, 31.3MB)
테스트 6 〉	통과 (0.56ms, 31.4MB)
테스트 7 〉	통과 (3.39ms, 31.3MB)
테스트 8 〉	통과 (2.36ms, 31.1MB)
테스트 9 〉	통과 (3.31ms, 32MB)
테스트 10 〉	통과 (7.16ms, 32.2MB)
테스트 11 〉	통과 (7.57ms, 32.7MB)
```