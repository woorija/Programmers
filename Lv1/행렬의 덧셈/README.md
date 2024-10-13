# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12950">행렬의 덧셈</a>

### 문제설명

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 

2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.

***

### 제한사항

 - 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.

***

### 답안
``` csharp
public class Solution {
    public int[,] solution(int[,] arr1, int[,] arr2) {
        int length1 = arr1.GetLength(0);
        int length2 = arr1.GetLength(1);
        int[,] answer = new int[length1,length2];
        for(int i = 0; i < length1; i++) {
            for(int j = 0; j < length2; j++) {
                answer[i,j] = arr1[i,j] + arr2[i,j];
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.28ms, 31.2MB)
테스트 2 〉	통과 (0.28ms, 31.2MB)
테스트 3 〉	통과 (0.32ms, 31.2MB)
테스트 4 〉	통과 (0.42ms, 31.6MB)
테스트 5 〉	통과 (0.28ms, 31.1MB)
테스트 6 〉	통과 (0.32ms, 31.2MB)
테스트 7 〉	통과 (0.29ms, 31.4MB)
테스트 8 〉	통과 (0.29ms, 31.2MB)
테스트 9 〉	통과 (0.36ms, 32.1MB)
테스트 10 〉	통과 (0.34ms, 31.9MB)
테스트 11 〉	통과 (0.30ms, 31.7MB)
테스트 12 〉	통과 (0.33ms, 31.7MB)
테스트 13 〉	통과 (0.35ms, 31.8MB)
테스트 14 〉	통과 (0.33ms, 31.6MB)
테스트 15 〉	통과 (0.33ms, 31.8MB)
테스트 16 〉	통과 (0.35ms, 31.8MB)
테스트 17 〉	통과 (2.18ms, 53MB)
```