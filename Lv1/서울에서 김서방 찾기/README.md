# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12919">서울에서 김서방 찾기</a>

### 문제설명

String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요. 
seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.

***

### 제한사항

 - seoul은 길이 1 이상, 1000 이하인 배열입니다.
 - seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.
 - "Kim"은 반드시 seoul 안에 포함되어 있습니다.

***

### 답안
``` csharp
public class Solution {
    public string solution(string[] seoul) {
        int index = 0;
        for(int i = 0; i < seoul.Length; i++) {
            if(seoul[i] == "Kim") {
                index = i;
                break;
            }
        }
        string answer = "김서방은 " + index + "에 있다";
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.31ms, 31.1MB)
테스트 2 〉	통과 (0.33ms, 31.2MB)
테스트 3 〉	통과 (0.41ms, 31.1MB)
테스트 4 〉	통과 (0.34ms, 31.3MB)
테스트 5 〉	통과 (0.33ms, 30.8MB)
테스트 6 〉	통과 (0.31ms, 31.3MB)
테스트 7 〉	통과 (0.31ms, 31.2MB)
테스트 8 〉	통과 (0.46ms, 31.2MB)
테스트 9 〉	통과 (0.30ms, 31.1MB)
테스트 10 〉	통과 (0.31ms, 31.3MB)
테스트 11 〉	통과 (0.36ms, 30.9MB)
테스트 12 〉	통과 (0.36ms, 31.1MB)
테스트 13 〉	통과 (0.33ms, 31MB)
```