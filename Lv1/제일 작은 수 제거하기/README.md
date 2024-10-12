# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12935">제일 작은 수 제거하기</a>

### 문제설명

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 

예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

***

### 제한사항

 - arr은 길이 1 이상인 배열입니다.
 - 인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.

***

### 답안
``` csharp
public class Solution {
    public int[] solution(int[] arr) {
        int[] answer;
        if(arr.Length == 1) {
            answer = new int[1] { -1 };
            return answer;
        }else{
            answer = new int[arr.Length - 1];
            int index = 0;
            for(int i = 1; i < arr.Length; i++) {
                if(arr[index] > arr[i]) {
                    index = i;
                }
            }
            for(int i = 0; i < index; i++) {
                answer[i] = arr[i];
            }
            for(int i = index + 1; i < arr.Length; i++) {
                answer[i - 1] = arr[i];
            }
            return answer;
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.42ms, 34.2MB)
테스트 2 〉	통과 (0.20ms, 31.3MB)
테스트 3 〉	통과 (0.21ms, 31.5MB)
테스트 4 〉	통과 (0.21ms, 31.6MB)
테스트 5 〉	통과 (0.24ms, 31.2MB)
테스트 6 〉	통과 (0.20ms, 31.5MB)
테스트 7 〉	통과 (0.23ms, 31.6MB)
테스트 8 〉	통과 (0.20ms, 31.2MB)
테스트 9 〉	통과 (0.20ms, 31.4MB)
테스트 10 〉	통과 (0.21ms, 31.2MB)
테스트 11 〉	통과 (0.20ms, 31.4MB)
테스트 12 〉	통과 (0.20ms, 31.2MB)
테스트 13 〉	통과 (0.21ms, 31.5MB)
테스트 14 〉	통과 (0.22ms, 31.4MB)
테스트 15 〉	통과 (0.21ms, 31.5MB)
테스트 16 〉	통과 (0.21ms, 31.5MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (0.29ms, 30.9MB)
테스트 2 〉	통과 (0.28ms, 31.3MB)
테스트 3 〉	통과 (0.28ms, 31.2MB)
테스트 4 〉	통과 (0.28ms, 30.9MB)
테스트 5 〉	통과 (0.30ms, 31.2MB)
테스트 6 〉	통과 (0.28ms, 31.1MB)
```