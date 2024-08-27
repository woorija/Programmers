# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12939">최대값과 최솟값</a>

### 문제설명

문자열 s에는 공백으로 구분된 숫자들이 저장되어 있습니다. str에 나타나는 숫자 중 최소값과 최대값을 찾아 이를 "(최소값) (최대값)"형태의 문자열을 반환하는 함수, solution을 완성하세요.
예를들어 s가 "1 2 3 4"라면 "1 4"를 리턴하고, "-1 -2 -3 -4"라면 "-4 -1"을 리턴하면 됩니다.

***

### 제한사항

 - s에는 둘 이상의 정수가 공백으로 구분되어 있습니다.

***

### 답안
``` csharp
using System.Collections.Generic;

public class Solution {
    public string solution(string s) {
        string answer = "";
        string[] sub = s.Split(" ");
        List<int> valueList = new List<int>(sub.Length);
        for(int i = 0; i < sub.Length; i++) {
            valueList.Add(int.Parse(sub[i]));
        }
        valueList.Sort();
        answer = valueList[0] + " " + valueList[sub.Length - 1];
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.37ms, 31.1MB)
테스트 2 〉	통과 (2.34ms, 31.6MB)
테스트 3 〉	통과 (2.23ms, 31.1MB)
테스트 4 〉	통과 (2.27ms, 31.2MB)
테스트 5 〉	통과 (2.45ms, 31.5MB)
테스트 6 〉	통과 (2.60ms, 31.4MB)
테스트 7 〉	통과 (2.15ms, 31.3MB)
테스트 8 〉	통과 (2.38ms, 31.2MB)
테스트 9 〉	통과 (2.41ms, 31.3MB)
테스트 10 〉	통과 (2.31ms, 31.4MB)
테스트 11 〉	통과 (2.24ms, 31.2MB)
테스트 12 〉	통과 (2.43ms, 31.5MB)
```