# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87390">n^2 배열 자르기</a>

### 문제설명

정수 n, left, right가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

 1. n행 n열 크기의 비어있는 2차원 배열을 만듭니다.
 2. i = 1, 2, 3, ..., n에 대해서, 다음 과정을 반복합니다.
   - 1행 1열부터 i행 i열까지의 영역 내의 모든 빈 칸을 숫자 i로 채웁니다.
 3. 1행, 2행, ..., n행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.
 4. 새로운 1차원 배열을 arr이라 할 때, arr[left], arr[left+1], ..., arr[right]만 남기고 나머지는 지웁니다.
정수 n, left, right가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ n ≤ 10^7
 - 0 ≤ left ≤ right < n^2
 - right - left < 10^5

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(int n, long left, long right) {
        int[] answer = new int[right-left+1];
        for(long i = left; i <= right; i++) {
            int min = (int)(i / n);
            int temp = (int)(i % n);
            if(temp < min){
                temp = min;
            }
            answer[i - left] = temp + 1;
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.90ms, 35.9MB)
테스트 2 〉	통과 (2.05ms, 37.4MB)
테스트 3 〉	통과 (2.01ms, 38MB)
테스트 4 〉	통과 (0.18ms, 31.2MB)
테스트 5 〉	통과 (0.18ms, 30.9MB)
테스트 6 〉	통과 (1.95ms, 36MB)
테스트 7 〉	통과 (2.09ms, 36.6MB)
테스트 8 〉	통과 (1.86ms, 36MB)
테스트 9 〉	통과 (1.94ms, 36.9MB)
테스트 10 〉	통과 (1.99ms, 36.7MB)
테스트 11 〉	통과 (1.94ms, 36.3MB)
테스트 12 〉	통과 (1.68ms, 36.2MB)
테스트 13 〉	통과 (1.87ms, 36.5MB)
테스트 14 〉	통과 (1.81ms, 36.3MB)
테스트 15 〉	통과 (1.72ms, 36.5MB)
테스트 16 〉	통과 (1.81ms, 37MB)
테스트 17 〉	통과 (1.86ms, 37MB)
테스트 18 〉	통과 (2.01ms, 37.8MB)
테스트 19 〉	통과 (1.91ms, 37.6MB)
테스트 20 〉	통과 (1.67ms, 36.9MB)
```