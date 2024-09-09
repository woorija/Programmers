# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/68936">쿼드압축 후 개수 세기</a>

### 문제설명

0과 1로 이루어진 2^n x 2^n 크기의 2차원 정수 배열 arr이 있습니다. 당신은 이 arr을 쿼드 트리와 같은 방식으로 압축하고자 합니다. 구체적인 방식은 다음과 같습니다.

 1. 당신이 압축하고자 하는 특정 영역을 S라고 정의합니다.
 2. 만약 S 내부에 있는 모든 수가 같은 값이라면, S를 해당 수 하나로 압축시킵니다.
 3. 그렇지 않다면, S를 정확히 4개의 균일한 정사각형 영역(입출력 예를 참고해주시기 바랍니다.)으로 쪼갠 뒤, 각 정사각형 영역에 대해 같은 방식의 압축을 시도합니다.

arr이 매개변수로 주어집니다. 위와 같은 방식으로 arr을 압축했을 때, 배열에 최종적으로 남는 0의 개수와 1의 개수를 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - arr의 행의 개수는 1 이상 1024 이하이며, 2의 거듭 제곱수 형태를 하고 있습니다. 즉, arr의 행의 개수는 1, 2, 4, 8, ..., 1024 중 하나입니다.
   - arr의 각 행의 길이는 arr의 행의 개수와 같습니다. 즉, arr은 정사각형 배열입니다.
   - arr의 각 행에 있는 모든 값은 0 또는 1 입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int[] answer;
    public int[] solution(int[,] arr) {
        answer = new int[2];
        for(int i = 0; i < arr.GetLength(0); i++) {
            for(int j = 0; j < arr.GetLength(1); j++) {
                if(arr[i,j] == 0){
                    answer[0]++;
                }else{
                    answer[1]++;
                }
            }
        }
        if(answer[0] == 0) {
            return new int[] { 0, 1 };
        }
        if(answer[1] == 0) {
            return new int[]{ 1, 0 };
        }
        int end = arr.GetLength(0);
        int middle = end / 2;
        quad(arr, 0, middle, 0, middle);
        quad(arr, middle, end, 0, middle);
        quad(arr, middle, end, middle, end);
        quad(arr, 0, middle, middle, end);
        return answer;
    }
    void quad(int[,] arr, int _startX, int _endX, int _startY, int _endY) {
        int count = 0;
        int middleX = _endX - (_endX - _startX) / 2;
        int middleY = _endY - (_endY - _startY) / 2;
        for(int i = _startX; i < _endX; i++) {
            for(int j = _startY; j < _endY; j++) {
                count += arr[i,j];
            }
        }
        int result = (_endX - _startX) * (_endX - _startX);
        if(count == 0) {
            answer[0] -= result - 1;
        }else if(count == result) {
            answer[1] -= result - 1;
        }else{
            if(_endX - middleX != 1) {
                quad(arr, _startX, middleX, _startY, middleY);
                quad(arr, middleX, _endX, _startY, middleY);
                quad(arr, middleX, _endX, middleY, _endY);
                quad(arr, _startX, middleX, middleY, _endY);
            }
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.53ms, 31MB)
테스트 2 〉	통과 (0.50ms, 31.4MB)
테스트 3 〉	통과 (0.49ms, 31MB)
테스트 4 〉	통과 (0.49ms, 31.2MB)
테스트 5 〉	통과 (23.55ms, 37.5MB)
테스트 6 〉	통과 (11.98ms, 37.8MB)
테스트 7 〉	통과 (12.04ms, 38MB)
테스트 8 〉	통과 (11.33ms, 37.9MB)
테스트 9 〉	통과 (10.21ms, 37.9MB)
테스트 10 〉	통과 (46.94ms, 55.4MB)
테스트 11 〉	통과 (0.47ms, 31.3MB)
테스트 12 〉	통과 (0.49ms, 31.1MB)
테스트 13 〉	통과 (10.24ms, 38.1MB)
테스트 14 〉	통과 (44.82ms, 55MB)
테스트 15 〉	통과 (56.36ms, 55.4MB)
테스트 16 〉	통과 (13.57ms, 38.1MB)
```