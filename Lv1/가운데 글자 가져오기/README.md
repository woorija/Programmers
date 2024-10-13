# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12903">가운데 글자 가져오기</a>

### 문제설명

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두글자를 반환하면 됩니다.

***

### 제한사항

 - s는 길이가 1 이상, 100이하인 스트링입니다.

***

### 답안
``` csharp
public class Solution {
    public string solution(string s) {
        string answer = "";
        int length = s.Length;
        
        if(length % 2 != 0) {
            answer = s.Substring(length / 2, 1);
        }else{
            answer = s.Substring(length / 2 - 1, 2);
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```

테스트 1 〉	통과 (0.19ms, 31.3MB)
테스트 2 〉	통과 (0.19ms, 31.1MB)
테스트 3 〉	통과 (0.25ms, 31.1MB)
테스트 4 〉	통과 (0.18ms, 31.2MB)
테스트 5 〉	통과 (0.17ms, 30.8MB)
테스트 6 〉	통과 (0.18ms, 31MB)
테스트 7 〉	통과 (0.17ms, 31.1MB)
테스트 8 〉	통과 (0.18ms, 31.2MB)
테스트 9 〉	통과 (0.19ms, 31MB)
테스트 10 〉	통과 (0.17ms, 31.3MB)
테스트 11 〉	통과 (0.18ms, 31.2MB)
테스트 12 〉	통과 (0.17ms, 31MB)
테스트 13 〉	통과 (0.19ms, 30.7MB)
테스트 14 〉	통과 (0.17ms, 30.8MB)
테스트 15 〉	통과 (0.19ms, 31MB)
테스트 16 〉	통과 (0.17ms, 30.9MB)
```