# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12944">평균 구하기</a>

### 문제설명

정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.

***

### 제한사항

 - arr은 길이 1 이상, 100 이하인 배열입니다.
 - arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.

***

### 답안
``` csharp
public class Solution {
    public double solution(int[] arr) {
        double answer = 0;
        for(int i = 0; i < arr.Length; i++) {
            answer += arr[i];
        }
        answer /= arr.Length;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.16ms, 31.6MB)
테스트 2 〉	통과 (0.17ms, 31.2MB)
테스트 3 〉	통과 (0.17ms, 31.6MB)
테스트 4 〉	통과 (0.16ms, 31MB)
테스트 5 〉	통과 (0.17ms, 31.6MB)
테스트 6 〉	통과 (0.16ms, 31.6MB)
테스트 7 〉	통과 (0.16ms, 31.3MB)
테스트 8 〉	통과 (0.19ms, 31.3MB)
테스트 9 〉	통과 (0.18ms, 31MB)
테스트 10 〉	통과 (0.16ms, 31.5MB)
테스트 11 〉	통과 (0.16ms, 31.5MB)
테스트 12 〉	통과 (0.17ms, 31.5MB)
테스트 13 〉	통과 (0.16ms, 31.4MB)
테스트 14 〉	통과 (0.16ms, 31.3MB)
테스트 15 〉	통과 (0.18ms, 31.4MB)
```