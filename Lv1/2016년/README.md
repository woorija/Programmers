# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12901">2016년</a>

### 문제설명

2016년 1월 1일은 금요일입니다. 2016년 a월 b일은 무슨 요일일까요? 두 수 a ,b를 입력받아 2016년 a월 b일이 무슨 요일인지 리턴하는 함수, solution을 완성하세요. 

요일의 이름은 일요일부터 토요일까지 각각 SUN,MON,TUE,WED,THU,FRI,SAT 입니다. 

예를 들어 a=5, b=24라면 5월 24일은 화요일이므로 문자열 "TUE"를 반환하세요.

***

### 제한사항

 - 2016년은 윤년입니다.
 - 2016년 a월 b일은 실제로 있는 날입니다. (13월 26일이나 2월 45일같은 날짜는 주어지지 않습니다)

***

### 답안
``` csharp
public class Solution {
    public string solution(int a, int b) {
        int count = b;
        int[] month = new int[11] { 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30 };
        string[] day = new string[7] { "THU", "FRI", "SAT", "SUN", "MON", "TUE", "WED" };
        string answer = "";
        
        for(int i = 0; i < a - 1; i++) {
            count += month[i];
        }
        count %= 7;
        answer = day[count];
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.30ms, 31MB)
테스트 2 〉	통과 (0.22ms, 31MB)
테스트 3 〉	통과 (0.23ms, 30.9MB)
테스트 4 〉	통과 (0.21ms, 31.2MB)
테스트 5 〉	통과 (0.22ms, 31.2MB)
테스트 6 〉	통과 (0.22ms, 31MB)
테스트 7 〉	통과 (0.23ms, 30.8MB)
테스트 8 〉	통과 (0.23ms, 31MB)
테스트 9 〉	통과 (0.23ms, 31.1MB)
테스트 10 〉	통과 (0.22ms, 31.2MB)
테스트 11 〉	통과 (0.25ms, 31MB)
테스트 12 〉	통과 (0.22ms, 31MB)
테스트 13 〉	통과 (0.24ms, 31.1MB)
테스트 14 〉	통과 (0.23ms, 31.1MB)
```