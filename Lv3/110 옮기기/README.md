# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/77886">110 옮기기</a>

### 문제설명

0과 1로 이루어진 어떤 문자열 x에 대해서, 당신은 다음과 같은 행동을 통해 x를 최대한 사전 순으로 앞에 오도록 만들고자 합니다.

 - x에 있는 "110"을 뽑아서, 임의의 위치에 다시 삽입합니다.

예를 들어, x = "11100" 일 때, 여기서 중앙에 있는 "110"을 뽑으면 x = "10" 이 됩니다. 뽑았던 "110"을 x의 맨 앞에 다시 삽입하면 x = "11010" 이 됩니다.

변형시킬 문자열 x가 여러 개 들어있는 문자열 배열 s가 주어졌을 때, 각 문자열에 대해서 위의 행동으로 변형해서 만들 수 있는 문자열 중 사전 순으로 가장 앞에 오는 문자열을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ s의 길이 ≤ 1,000,000
 - 1 ≤ s의 각 원소 길이 ≤ 1,000,000
 - 1 ≤ s의 모든 원소의 길이의 합 ≤ 1,000,000

***

### 답안
``` csharp
using System;
using System.Text;
using System.Collections.Generic;

public class Solution {
    public string[] solution(string[] s) {
        string[] answer = new string[s.Length];
        
        for(int i = 0; i < s.Length; i++) {
            StringBuilder sb = new StringBuilder();
            int count=0;
            
            for(int j = 0; j < s[i].Length; j++) {
                sb.Append(s[i][j]);
                
                if(sb.Length >= 3 && sb[sb.Length - 3] == '1' && sb[sb.Length - 2] == '1' && sb[sb.Length - 1] == '0' ) {
                    sb.Remove(sb.Length - 3, 3);
                    count++;
                }
            }
            
            string temp = sb.ToString();
            int index = temp.LastIndexOf('0');
            
            sb.Clear();
            
            if(index != -1) {
                sb.Append(temp.Substring(0, index + 1));
            }
            for(int j = 0; j < count; j++) {
                sb.Append("110");
            }
            sb.Append(temp.Substring(index + 1));
            answer[i] = sb.ToString();
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (36.75ms, 44.7MB)
테스트 2 〉	통과 (29.15ms, 43.5MB)
테스트 3 〉	통과 (25.67ms, 39.7MB)
테스트 4 〉	통과 (29.74ms, 43.4MB)
테스트 5 〉	통과 (32.86ms, 43.7MB)
테스트 6 〉	통과 (32.30ms, 42.9MB)
테스트 7 〉	통과 (22.95ms, 39MB)
테스트 8 〉	통과 (17.26ms, 36.4MB)
테스트 9 〉	통과 (43.11ms, 57.6MB)
테스트 10 〉	통과 (40.43ms, 55.7MB)
테스트 11 〉	통과 (49.53ms, 55.3MB)
테스트 12 〉	통과 (63.02ms, 55.1MB)
테스트 13 〉	통과 (45.13ms, 55.4MB)
테스트 14 〉	통과 (45.30ms, 55MB)
테스트 15 〉	통과 (46.57ms, 55.2MB)
테스트 16 〉	통과 (43.35ms, 54.9MB)
테스트 17 〉	통과 (44.34ms, 53.3MB)
테스트 18 〉	통과 (33.66ms, 42MB)
테스트 19 〉	통과 (36.81ms, 42.6MB)
테스트 20 〉	통과 (31.51ms, 40.3MB)
테스트 21 〉	통과 (43.13ms, 41.8MB)
```