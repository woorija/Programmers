# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42746">가장 큰 수</a>

### 문제설명

0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - numbers의 길이는 1 이상 100,000 이하입니다.
 - numbers의 원소는 0 이상 1,000 이하입니다.
 - 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

***

### 답안
``` csharp
using System;
using System.Text;

public class Solution {
    public string solution(int[] numbers) {
        string[] arr = new string[numbers.Length];
        for(int i = 0; i < arr.Length; i++) {
            arr[i] = numbers[i].ToString();
        }
        Array.Sort(arr, (x, y) => (y + x).CompareTo(x + y));
        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < arr.Length; i++) {
            sb.Append(arr[i]);
        }
        string str = sb.ToString();
        if(str.Replace("0", "") == "") {
            return "0";
        }
        return sb.ToString();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (997.79ms, 41.8MB)
테스트 2 〉	통과 (501.77ms, 38.9MB)
테스트 3 〉	통과 (1239.67ms, 44.1MB)
테스트 4 〉	통과 (26.61ms, 34MB)
테스트 5 〉	통과 (841.77ms, 41.2MB)
테스트 6 〉	통과 (836.13ms, 40.5MB)
테스트 7 〉	통과 (4.70ms, 31.6MB)
테스트 8 〉	통과 (3.77ms, 31.7MB)
테스트 9 〉	통과 (3.81ms, 31.8MB)
테스트 10 〉	통과 (3.89ms, 31.6MB)
테스트 11 〉	통과 (3.87ms, 31.8MB)
테스트 12 〉	통과 (4.98ms, 31.8MB)
테스트 13 〉	통과 (4.63ms, 31.7MB)
테스트 14 〉	통과 (4.65ms, 31.7MB)
테스트 15 〉	통과 (4.05ms, 31.8MB)
```