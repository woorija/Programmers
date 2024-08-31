# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12949">행렬의 곱셈</a>

### 문제설명

2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

***

### 제한사항

 - 행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
 - 행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
 - 곱할 수 있는 배열만 주어집니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int[,] answer;
    public int[,] solution(int[,] arr1, int[,] arr2) {
        int row = arr1.GetLength(0);
        int col = arr2.Length / arr2.GetLength(0);
        answer = new int[row, col];
        for(int i = 0;i < row; i++) {
            for(int j = 0; j < col; j++) {
                answer[i,j] = Calc(arr1, arr2, i, j);
            }
        }
        return answer;
    }
    int Calc(int[,] arr1, int[,] arr2, int row, int col) {
        int value = 0;
        for(int i = 0; i < arr2.GetLength(0); i++) {
            value += arr1[row,i] * arr2[i,col];
        }
        return value;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.40ms, 31.5MB)
테스트 2 〉	통과 (2.63ms, 31.8MB)
테스트 3 〉	통과 (2.84ms, 31.8MB)
테스트 4 〉	통과 (0.34ms, 31.3MB)
테스트 5 〉	통과 (1.99ms, 31.8MB)
테스트 6 〉	통과 (1.24ms, 31.8MB)
테스트 7 〉	통과 (0.33ms, 31.3MB)
테스트 8 〉	통과 (0.31ms, 31.4MB)
테스트 9 〉	통과 (0.30ms, 31.3MB)
테스트 10 〉	통과 (2.00ms, 31.6MB)
테스트 11 〉	통과 (0.44ms, 31.5MB)
테스트 12 〉	통과 (0.31ms, 31.6MB)
테스트 13 〉	통과 (1.57ms, 31.6MB)
테스트 14 〉	통과 (2.90ms, 31.6MB)
테스트 15 〉	통과 (1.11ms, 31.4MB)
테스트 16 〉	통과 (0.58ms, 31.5MB)
```