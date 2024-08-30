# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12953">N개의 최소공배수</a>

### 문제설명

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

***

### 제한사항

 - arr은 길이 1이상, 15이하인 배열입니다.
 - arr의 원소는 100 이하인 자연수입니다.

***

### 답안
``` csharp
public class Solution {
    public int solution(int[] arr) {
        int answer = 0;
        if(arr.Length == 1) {
            return arr[0];
        }
        answer = arr[0];
        for(int i = 1; i < arr.Length; i++) {
            answer = lcm(answer, arr[i]);
        }
        
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
테스트 1 〉	통과 (0.25ms, 31.4MB)
테스트 2 〉	통과 (0.28ms, 31.3MB)
테스트 3 〉	통과 (0.28ms, 31.6MB)
테스트 4 〉	통과 (0.29ms, 31.4MB)
테스트 5 〉	통과 (0.43ms, 31.4MB)
테스트 6 〉	통과 (0.26ms, 31.1MB)
테스트 7 〉	통과 (0.26ms, 31.3MB)
테스트 8 〉	통과 (0.27ms, 31MB)
테스트 9 〉	통과 (0.26ms, 31.1MB)
테스트 10 〉	통과 (0.25ms, 31.4MB)
```