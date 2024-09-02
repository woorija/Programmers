# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42747">H-Index</a>

### 문제설명

H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
 - 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        int[] sortCitations = citations;
        Array.Sort(sortCitations);
        int length = sortCitations.Length;
        for(int i = 0; i < length; i++) {
            if(sortCitations[i] >= length - i) {
                answer = length-i;
                break;
            }
            
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.72ms, 31.6MB)
테스트 2 〉	통과 (1.63ms, 31.3MB)
테스트 3 〉	통과 (1.74ms, 31.5MB)
테스트 4 〉	통과 (2.53ms, 31.6MB)
테스트 5 〉	통과 (1.74ms, 31.6MB)
테스트 6 〉	통과 (1.61ms, 31.3MB)
테스트 7 〉	통과 (1.59ms, 31.3MB)
테스트 8 〉	통과 (1.54ms, 31.4MB)
테스트 9 〉	통과 (1.62ms, 31.6MB)
테스트 10 〉	통과 (1.57ms, 31.3MB)
테스트 11 〉	통과 (1.64ms, 31.4MB)
테스트 12 〉	통과 (1.53ms, 31MB)
테스트 13 〉	통과 (1.60ms, 31.3MB)
테스트 14 〉	통과 (1.69ms, 31.5MB)
테스트 15 〉	통과 (1.71ms, 31.4MB)
테스트 16 〉	통과 (1.39ms, 31.3MB)
```