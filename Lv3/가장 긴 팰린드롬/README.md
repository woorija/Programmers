# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12904">가장 긴 팰린드롬</a>

### 문제설명

앞뒤를 뒤집어도 똑같은 문자열을 팰린드롬(palindrome)이라고 합니다.

문자열 s가 주어질 때, s의 부분문자열(Substring)중 가장 긴 팰린드롬의 길이를 return 하는 solution 함수를 완성해 주세요.

예를들면, 문자열 s가 "abcdcba"이면 7을 return하고 "abacde"이면 3을 return합니다.

***

### 제한사항

 - 문자열 s의 길이 : 2,500 이하의 자연수
 - 문자열 s는 알파벳 소문자로만 구성

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string s) {
        int answer = 0;
        char[] arr = s.ToCharArray();
        
        for(int i = 0; i < arr.Length; i++) {
            int count = PalindromeCount(arr, i, false);
            answer = Math.Max(answer, count);
            
            if(i != arr.Length - 1 && arr[i] == arr[i + 1]) {
                count = PalindromeCount(arr, i, true);
                answer = Math.Max(answer, count);
            }
        }
        
        return answer;
    }
    
    int PalindromeCount(char[] _arr, int _index, bool _isPair) {
        int count;
        int prevIndex = _index - 1;
        int nextIndex;
        
        if(_isPair){
            count = 2;
            nextIndex = _index + 2;
        }else{
            count = 1;
            nextIndex = _index + 1;
        }
        
        while(prevIndex >= 0 && nextIndex < _arr.Length) {
            if(_arr[prevIndex] == _arr[nextIndex]) {
                count += 2;
                prevIndex--;
                nextIndex++;
            }else{
                break;
            }
        }
        
        return count;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.36ms, 31.3MB)
테스트 2 〉	통과 (0.35ms, 31.2MB)
테스트 3 〉	통과 (0.31ms, 31.2MB)
테스트 4 〉	통과 (0.34ms, 31.1MB)
테스트 5 〉	통과 (0.31ms, 31.4MB)
테스트 6 〉	통과 (0.30ms, 31.2MB)
테스트 7 〉	통과 (0.30ms, 31.5MB)
테스트 8 〉	통과 (0.32ms, 31.6MB)
테스트 9 〉	통과 (0.33ms, 31.4MB)
테스트 10 〉	통과 (0.31ms, 31.4MB)
테스트 11 〉	통과 (0.32ms, 31.3MB)
테스트 12 〉	통과 (0.33ms, 31.1MB)
테스트 13 〉	통과 (0.42ms, 31.1MB)
테스트 14 〉	통과 (0.34ms, 30.9MB)
테스트 15 〉	통과 (0.31ms, 31.5MB)
테스트 16 〉	통과 (0.34ms, 31.5MB)
테스트 17 〉	통과 (0.33ms, 31.6MB)
테스트 18 〉	통과 (0.38ms, 31.2MB)
테스트 19 〉	통과 (0.31ms, 30.9MB)
테스트 20 〉	통과 (0.33ms, 31.3MB)
테스트 21 〉	통과 (0.46ms, 31.2MB)
테스트 22 〉	통과 (0.34ms, 30.8MB)
테스트 23 〉	통과 (0.33ms, 31.2MB)
테스트 24 〉	통과 (0.34ms, 31.4MB)
```

### 효율성 테스트
```
테스트 1 〉	통과 (0.33ms, 31.4MB)
테스트 2 〉	통과 (3.24ms, 31.2MB)
```