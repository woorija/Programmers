# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/81301">숫자 문자열과 영단어</a>

### 문제설명

네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

 - 1478 → "one4seveneight"
 - 234567 → "23four5six7"
 - 10203 → "1zerotwozero3"

이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

참고로 각 숫자에 대응되는 영단어는 다음 표와 같습니다.

| 숫자 | 영단어 |
| ------- | ------- |
| 0 | zero |
| 1 | one |
| 2 | two |
| 3 | three |
| 4 | four |
| 5 | five |
| 6 | six |
| 7 | seven |
| 8 | eight |
| 9 | nine |

***

### 제한사항

 - 1 ≤ s의 길이 ≤ 50
 - s가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않습니다.
 - return 값이 1 이상 2,000,000,000 이하의 정수가 되는 올바른 입력만 s로 주어집니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string s) {
        string str = s.Replace("zero","0").Replace("one","1").Replace("two","2").Replace("three","3").Replace("four","4").Replace("five","5").Replace("six","6").Replace("seven","7").Replace("eight","8").Replace("nine","9");
        int answer = int.Parse(str);
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.93ms, 31.8MB)
테스트 2 〉	통과 (0.87ms, 31.6MB)
테스트 3 〉	통과 (0.87ms, 31.5MB)
테스트 4 〉	통과 (0.91ms, 31.7MB)
테스트 5 〉	통과 (0.87ms, 31.8MB)
테스트 6 〉	통과 (0.94ms, 31.7MB)
테스트 7 〉	통과 (0.89ms, 31.5MB)
테스트 8 〉	통과 (0.88ms, 31.7MB)
테스트 9 〉	통과 (0.87ms, 31.6MB)
테스트 10 〉	통과 (0.69ms, 31.9MB)
```