# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12927">야근 지수</a>

### 문제설명

회사원 Demi는 가끔은 야근을 하는데요, 야근을 하면 야근 피로도가 쌓입니다. 야근 피로도는 야근을 시작한 시점에서 남은 일의 작업량을 제곱하여 더한 값입니다. Demi는 N시간 동안 야근 피로도를 최소화하도록 일할 겁니다.Demi가 1시간 동안 작업량 1만큼을 처리할 수 있다고 할 때, 퇴근까지 남은 N 시간과 각 일에 대한 작업량 works에 대해 야근 피로도를 최소화한 값을 리턴하는 함수 solution을 완성해주세요.

***

### 제한사항

 - works는 길이 1 이상, 20,000 이하인 배열입니다.
 - works의 원소는 50000 이하인 자연수입니다.
 - n은 1,000,000 이하인 자연수입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public long solution(int n, int[] works) {
        long answer = 0;
        int count = n;
        int index = 1;
        int length = works.Length;
        Array.Sort(works);

        while(count > 0){
            if(length != index){
                for(int i = length - index - 1; i >= 0; i--) {
                    if(works[i] == works[i + 1]) {
                        index++;
                    }else{
                        break;
                    }
                }
            }
            
            int reduce = 0;
            if(length == index) {
                reduce = (int)Math.Ceiling((double)count / n);
            }else{
                reduce = works[length - index] - works[length - index - 1];
            }
            for(int i = length - 1; i >= length - index; i--) {
                works[i] -= reduce;
                count -= reduce;
            }
        }
        while(count < 0) {
            for(int i = length - 1; i >= length - index; i--) {
                works[i]++;
                count++;
                if(count == 0) {
                    break;
                }
            }
        }
        
        for(int i = 0; i < length; i++) {
            if(works[i] > 0) {
                answer += (long)works[i] * (long)works[i];
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.63ms, 31MB)
테스트 2 〉	통과 (1.47ms, 31.3MB)
테스트 3 〉	통과 (1.47ms, 31.3MB)
테스트 4 〉	통과 (1.45ms, 31.1MB)
테스트 5 〉	통과 (1.48ms, 31.6MB)
테스트 6 〉	통과 (1.44ms, 31.4MB)
테스트 7 〉	통과 (1.44ms, 31.3MB)
테스트 8 〉	통과 (1.98ms, 31.2MB)
테스트 9 〉	통과 (1.75ms, 31.3MB)
테스트 10 〉	통과 (1.62ms, 31.3MB)
테스트 11 〉	통과 (1.50ms, 31.3MB)
테스트 12 〉	통과 (1.56ms, 31.5MB)
테스트 13 〉	통과 (1.57ms, 30.9MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (2.37ms, 31.3MB)
테스트 2 〉	통과 (1.82ms, 30.9MB)
```