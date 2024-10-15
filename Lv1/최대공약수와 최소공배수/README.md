# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12940">최대공약수와 최소공배수</a>

### 문제설명

두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 

예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

***

### 제한사항

 - 두 수는 1이상 1000000이하의 자연수입니다.

***

### 답안
``` csharp
public class Solution {
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        answer[0] = gdc(n, m);
        answer[1] = lcm(n, m);
        return answer;
    }
    int gdc(int a, int b){
        if(b == 0) {
            return a;
        }else{
            return gdc(b, a % b);
        }
    }
    int lcm(int a, int b){
        return a * b / gdc(a, b);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.23ms, 31.3MB)
테스트 2 〉	통과 (0.23ms, 31.4MB)
테스트 3 〉	통과 (0.21ms, 31.3MB)
테스트 4 〉	통과 (0.21ms, 31.3MB)
테스트 5 〉	통과 (0.23ms, 31.4MB)
테스트 6 〉	통과 (0.23ms, 31MB)
테스트 7 〉	통과 (0.21ms, 31.2MB)
테스트 8 〉	통과 (0.21ms, 31.5MB)
테스트 9 〉	통과 (0.25ms, 31.4MB)
테스트 10 〉	통과 (0.22ms, 31.4MB)
테스트 11 〉	통과 (0.22ms, 31.4MB)
테스트 12 〉	통과 (0.27ms, 31.6MB)
테스트 13 〉	통과 (0.23ms, 31.3MB)
테스트 14 〉	통과 (0.23ms, 31.4MB)
테스트 15 〉	통과 (0.22ms, 31.4MB)
테스트 16 〉	통과 (0.31ms, 31.5MB)
```