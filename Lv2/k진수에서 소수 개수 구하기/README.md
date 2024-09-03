# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/92335">k진수에서 소수 개수 구하기</a>

### 문제설명

양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

 - 0P0처럼 소수 양쪽에 0이 있는 경우
 - P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
 - 0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
 - P처럼 소수 양쪽에 아무것도 없는 경우
 - 단, P는 각 자릿수에 0을 포함하지 않는 소수입니다.
   - 예를 들어, 101은 P가 될 수 없습니다.
예를 들어, 437674을 3진수로 바꾸면 211020101011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

***

### 제한사항

 - 1 ≤ n ≤ 1,000,000
 - 3 ≤ k ≤ 10

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int n, int k) {
        string str = "";
        int num = n;
        while(num > k){
            str = str.Insert(0, (num % k).ToString());
            num /= k;
        }
        str = str.Insert(0, num.ToString());
        // 진수 변환 완료
        string[] arr = str.Split("0");
        int answer = 0;
        for(int i = 0; i < arr.Length; i++) {
            if(IsPrime(arr[i])) {
                answer++;
            }
        }
        
        return answer;
    }
    bool IsPrime(string _str) {
        if(_str == "" || _str == "1") {
            return false;
        }
        if(_str == "2") {
            return true;
        }
        // 1, 2 예외처리
        long num = long.Parse(_str);
        int sqrtNum = (int)Math.Sqrt(num);
        for(int i = 2; i <= sqrtNum + 1; i++) {
            if(num % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (9.59ms, 31.3MB)
테스트 2 〉	통과 (0.92ms, 31.2MB)
테스트 3 〉	통과 (0.94ms, 31.1MB)
테스트 4 〉	통과 (1.44ms, 31.6MB)
테스트 5 〉	통과 (0.98ms, 31.5MB)
테스트 6 〉	통과 (0.59ms, 30.9MB)
테스트 7 〉	통과 (0.93ms, 31.5MB)
테스트 8 〉	통과 (0.62ms, 31.1MB)
테스트 9 〉	통과 (0.98ms, 31.3MB)
테스트 10 〉	통과 (0.98ms, 31.5MB)
테스트 11 〉	통과 (0.95ms, 31.5MB)
테스트 12 〉	통과 (0.97ms, 31.6MB)
테스트 13 〉	통과 (0.98ms, 31.4MB)
테스트 14 〉	통과 (0.95ms, 31.5MB)
테스트 15 〉	통과 (0.96ms, 31.6MB)
```