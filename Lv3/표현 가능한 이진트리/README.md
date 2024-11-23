# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/150367">표현 가능한 이진트리</a>

### 문제설명

당신은 이진트리를 수로 표현하는 것을 좋아합니다.

이진트리를 수로 표현하는 방법은 다음과 같습니다.

 1. 이진수를 저장할 빈 문자열을 생성합니다.
 2. 주어진 이진트리에 더미 노드를 추가하여 포화 이진트리로 만듭니다. 루트 노드는 그대로 유지합니다.
 3. 만들어진 포화 이진트리의 노드들을 가장 왼쪽 노드부터 가장 오른쪽 노드까지, 왼쪽에 있는 순서대로 살펴봅니다. 노드의 높이는 살펴보는 순서에 영향을 끼치지 않습니다.
 4. 살펴본 노드가 더미 노드라면, 문자열 뒤에 0을 추가합니다. 살펴본 노드가 더미 노드가 아니라면, 문자열 뒤에 1을 추가합니다.
 5. 문자열에 저장된 이진수를 십진수로 변환합니다.

이진트리에서 리프 노드가 아닌 노드는 자신의 왼쪽 자식이 루트인 서브트리의 노드들보다 오른쪽에 있으며, 자신의 오른쪽 자식이 루트인 서브트리의 노드들보다 왼쪽에 있다고 가정합니다.

당신은 수가 주어졌을때, 하나의 이진트리로 해당 수를 표현할 수 있는지 알고 싶습니다.

이진트리로 만들고 싶은 수를 담은 1차원 정수 배열 numbers가 주어집니다. numbers에 주어진 순서대로 하나의 이진트리로 해당 수를 표현할 수 있다면 1을, 표현할 수 없다면 0을 1차원 정수 배열에 담아 return 하도록 solution 함수를 완성해주세요.
***

### 제한사항

 - 1 ≤ numbers의 길이 ≤ 10,000
   - 1 ≤ numbers의 원소 ≤ 1015

***

### 답안
``` csharp
using System;
using System.Text;

public class Solution {
    public int[] solution(long[] numbers) {
        int[] answer = new int[numbers.Length];
        
        for(int i = 0; i < numbers.Length; i++) {
            answer[i] = 1;
            string temp = Convert.ToString(numbers[i], 2);
            long digit = 1;
            
            while(temp.Length > digit - 1) {
                digit *= 2;
            }
            digit--;
            
            StringBuilder sb = new StringBuilder();
            
            for(long j = 0; j < digit - temp.Length; j++) {
                sb.Append('0');
            }
            sb.Append(temp);
            
            string num = sb.ToString();
            int rootIndex = (num.Length - 1) / 2;
            
            for(int j = 0; j < num.Length; j++) {
                int tempIndex = rootIndex;
                int move = (rootIndex + 1) / 2;
                
                if(num[j] == '1') {
                    while(tempIndex != j) {
                        if(num[tempIndex] == '0') {
                            answer[i] = 0;
                            break;
                        }
                        if(tempIndex < j) {
                            tempIndex += move;
                        }else{
                        tempIndex -= move;
                        }
                        move /= 2;
                    }
                }
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.48ms, 31.2MB)
테스트 2 〉	통과 (0.43ms, 31.1MB)
테스트 3 〉	통과 (0.42ms, 31.4MB)
테스트 4 〉	통과 (0.76ms, 31.5MB)
테스트 5 〉	통과 (0.52ms, 31MB)
테스트 6 〉	통과 (0.52ms, 31.4MB)
테스트 7 〉	통과 (0.57ms, 31.5MB)
테스트 8 〉	통과 (0.52ms, 31.1MB)
테스트 9 〉	통과 (1.50ms, 31.7MB)
테스트 10 〉	통과 (9.30ms, 34.7MB)
테스트 11 〉	통과 (10.48ms, 35MB)
테스트 12 〉	통과 (9.17ms, 34.8MB)
테스트 13 〉	통과 (8.71ms, 34.7MB)
테스트 14 〉	통과 (8.65ms, 34.4MB)
테스트 15 〉	통과 (6.49ms, 33.4MB)
테스트 16 〉	통과 (14.52ms, 34.8MB)
테스트 17 〉	통과 (14.90ms, 35.2MB)
테스트 18 〉	통과 (13.62ms, 35.1MB)
테스트 19 〉	통과 (12.36ms, 35.2MB)
테스트 20 〉	통과 (7.40ms, 34MB)
```