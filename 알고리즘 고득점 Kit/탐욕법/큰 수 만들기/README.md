# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42883">큰 수 만들기</a>

### 문제설명

어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

***

### 제한사항

 - number는 2자리 이상, 1,000,000자리 이하인 숫자입니다.
 = k는 1 이상 number의 자릿수 미만인 자연수입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;
using System.Text;

public class Solution {
    public string solution(string number, int k) {
        List<char> numbers = new List<char>();
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < number.Length; i++) {
            numbers.Add(number[i]);
        }
        int index = 0;
        for(int i = 0; i < k; i++) {
            bool check = false;
            for(int j = index; j < numbers.Count - 1; j++) {
                if(numbers[j] < numbers[j + 1]) {
                    index= j - 1 > 0 ? j - 1 : 0;
                    numbers.RemoveAt(j);
                    check = true;
                    break;
                }
            }
            if(!check) {
                numbers.RemoveAt(numbers.Count - 1);
            }
        }
        for(int i = 0; i < numbers.Count; i++) {
            sb.Append(numbers[i]);
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.79ms, 30.8MB)
테스트 2 〉	통과 (0.78ms, 30.8MB)
테스트 3 〉	통과 (0.78ms, 30.9MB)
테스트 4 〉	통과 (0.78ms, 31.1MB)
테스트 5 〉	통과 (0.80ms, 31MB)
테스트 6 〉	통과 (2.74ms, 31.1MB)
테스트 7 〉	통과 (22.79ms, 31.2MB)
테스트 8 〉	통과 (113.37ms, 32.2MB)
테스트 9 〉	통과 (10.21ms, 35.4MB)
테스트 10 〉	통과 (3589.43ms, 35.9MB)
테스트 11 〉	통과 (0.75ms, 30.8MB)
테스트 12 〉	통과 (0.76ms, 31MB)
```