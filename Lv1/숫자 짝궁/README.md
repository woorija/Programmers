# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/131128">숫자 짝궁</a>

### 문제설명

두 정수 X, Y의 임의의 자리에서 공통으로 나타나는 정수 k(0 ≤ k ≤ 9)들을 이용하여 만들 수 있는 가장 큰 정수를 두 수의 짝꿍이라 합니다(단, 공통으로 나타나는 정수 중 서로 짝지을 수 있는 숫자만 사용합니다). X, Y의 짝꿍이 존재하지 않으면, 짝꿍은 -1입니다. X, Y의 짝꿍이 0으로만 구성되어 있다면, 짝꿍은 0입니다.

예를 들어, X = 3403이고 Y = 13203이라면, X와 Y의 짝꿍은 X와 Y에서 공통으로 나타나는 3, 0, 3으로 만들 수 있는 가장 큰 정수인 330입니다. 다른 예시로 X = 5525이고 Y = 1255이면 X와 Y의 짝꿍은 X와 Y에서 공통으로 나타나는 2, 5, 5로 만들 수 있는 가장 큰 정수인 552입니다(X에는 5가 3개, Y에는 5가 2개 나타나므로 남는 5 한 개는 짝 지을 수 없습니다.)

두 정수 X, Y가 주어졌을 때, X, Y의 짝꿍을 return하는 solution 함수를 완성해주세요.

***

### 제한사항

 - 3 ≤ X, Y의 길이(자릿수) ≤ 3,000,000입니다.
 - X, Y는 0으로 시작하지 않습니다.
 - X, Y의 짝꿍은 상당히 큰 정수일 수 있으므로, 문자열로 반환합니다.

***

### 답안
``` csharp
using System;
using System.Text;

public class Solution {
    public string solution(string X, string Y) {
        StringBuilder sb = new StringBuilder();
        int[] countX = new int[10];
        int[] countY = new int[10];
        
        for(int i = 0; i < X.Length; i++) {
            countX[(int)(X[i] - '0')]++;
        }
        for(int i = 0; i < Y.Length; i++) {
            countY[(int)(Y[i] - '0')]++;
        }
        for(int i = 9; i >= 1; i--) {
            for(int j = 0; j < Math.Min(countX[i], countY[i]); j++) {
                sb.Append(i);
            }
        }
        int zero = Math.Min(countX[0], countY[0]);
        if(sb.Length == 0) {
            if(zero == 0) {
                sb.Append("-1");
            }else{
                sb.Append("0");
            }
        }else{
            for(int i = 0; i < zero; i++) {
                sb.Append("0");
            }
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.99ms, 31.6MB)
테스트 2 〉	통과 (0.99ms, 31MB)
테스트 3 〉	통과 (1.00ms, 31.2MB)
테스트 4 〉	통과 (0.94ms, 31.3MB)
테스트 5 〉	통과 (0.88ms, 31.3MB)
테스트 6 〉	통과 (0.86ms, 31.1MB)
테스트 7 〉	통과 (1.44ms, 31.1MB)
테스트 8 〉	통과 (1.55ms, 31.5MB)
테스트 9 〉	통과 (1.43ms, 31.2MB)
테스트 10 〉	통과 (1.34ms, 31.2MB)
테스트 11 〉	통과 (332.58ms, 64MB)
테스트 12 〉	통과 (231.37ms, 64MB)
테스트 13 〉	통과 (278.64ms, 64.1MB)
테스트 14 〉	통과 (200.04ms, 64.3MB)
테스트 15 〉	통과 (351.03ms, 64.1MB)
테스트 16 〉	통과 (0.61ms, 30.8MB)
테스트 17 〉	통과 (0.55ms, 30.9MB)
테스트 18 〉	통과 (0.38ms, 31.1MB)
테스트 19 〉	통과 (0.40ms, 31.1MB)
```