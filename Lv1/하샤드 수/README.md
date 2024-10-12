# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12947">하샤드 수</a>

### 문제설명

양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 

자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

***

### 제한사항

 - x는 1 이상, 10000 이하인 정수입니다.

***

### 답안
``` csharp
public class Solution {
    public bool solution(int x) {
        bool answer = false;
        string numStr = x.ToString();
        int num = 0;
        for(int i = 0; i < numStr.Length; i++) {
            num += int.Parse(numStr[i].ToString());
        }
        if(x % num == 0) {
            answer = true;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.83ms, 31.6MB)
테스트 2 〉	통과 (0.81ms, 31.5MB)
테스트 3 〉	통과 (0.81ms, 30.9MB)
테스트 4 〉	통과 (0.81ms, 31.3MB)
테스트 5 〉	통과 (0.80ms, 31.5MB)
테스트 6 〉	통과 (0.84ms, 31.4MB)
테스트 7 〉	통과 (0.79ms, 31.7MB)
테스트 8 〉	통과 (0.81ms, 31.1MB)
테스트 9 〉	통과 (0.85ms, 31.1MB)
테스트 10 〉	통과 (0.82ms, 31.6MB)
테스트 11 〉	통과 (0.80ms, 31.3MB)
테스트 12 〉	통과 (0.78ms, 31.2MB)
테스트 13 〉	통과 (0.83ms, 31.1MB)
테스트 14 〉	통과 (0.84ms, 31.1MB)
테스트 15 〉	통과 (0.79ms, 31.3MB)
테스트 16 〉	통과 (0.82ms, 31.4MB)
테스트 17 〉	통과 (0.89ms, 31.3MB)
```