# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/159994">카드 뭉치</a>

### 문제설명

코니는 영어 단어가 적힌 카드 뭉치 두 개를 선물로 받았습니다. 코니는 다음과 같은 규칙으로 카드에 적힌 단어들을 사용해 원하는 순서의 단어 배열을 만들 수 있는지 알고 싶습니다.

 - 원하는 카드 뭉치에서 카드를 순서대로 한 장씩 사용합니다.
 - 한 번 사용한 카드는 다시 사용할 수 없습니다.
 - 카드를 사용하지 않고 다음 카드로 넘어갈 수 없습니다.
 - 기존에 주어진 카드 뭉치의 단어 순서는 바꿀 수 없습니다.

예를 들어 첫 번째 카드 뭉치에 순서대로 ["i", "drink", "water"], 두 번째 카드 뭉치에 순서대로 ["want", "to"]가 적혀있을 때 ["i", "want", "to", "drink", "water"] 순서의 단어 배열을 만들려고 한다면 첫 번째 카드 뭉치에서 "i"를 사용한 후 두 번째 카드 뭉치에서 "want"와 "to"를 사용하고 첫 번째 카드뭉치에 "drink"와 "water"를 차례대로 사용하면 원하는 순서의 단어 배열을 만들 수 있습니다.

문자열로 이루어진 배열 cards1, cards2와 원하는 단어 배열 goal이 매개변수로 주어질 때, cards1과 cards2에 적힌 단어들로 goal를 만들 있다면 "Yes"를, 만들 수 없다면 "No"를 return하는 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ cards1의 길이, cards2의 길이 ≤ 10
   - 1 ≤ cards1[i]의 길이, cards2[i]의 길이 ≤ 10
   - cards1과 cards2에는 서로 다른 단어만 존재합니다.
 - 2 ≤ goal의 길이 ≤ cards1의 길이 + cards2의 길이
   - 1 ≤ goal[i]의 길이 ≤ 10
   - goal의 원소는 cards1과 cards2의 원소들로만 이루어져 있습니다.
 - cards1, cards2, goal의 문자열들은 모두 알파벳 소문자로만 이루어져 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public string solution(string[] cards1, string[] cards2, string[] goal) {
        int firstIndex = 0;
        int secondIndex = 0;
        string answer = "Yes";
        for(int i = 0; i < goal.Length; i++) {
            if(firstIndex != cards1.Length && goal[i] == cards1[firstIndex]) {
                firstIndex++;
            }else if(secondIndex != cards2.Length && goal[i] == cards2[secondIndex]) {
                secondIndex++;
            }else{
                answer = "No";
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
테스트 1 〉	통과 (0.21ms, 31MB)
테스트 2 〉	통과 (0.21ms, 30.9MB)
테스트 3 〉	통과 (0.21ms, 30.9MB)
테스트 4 〉	통과 (0.20ms, 31MB)
테스트 5 〉	통과 (0.33ms, 31.4MB)
테스트 6 〉	통과 (0.29ms, 31.2MB)
테스트 7 〉	통과 (0.33ms, 31.2MB)
테스트 8 〉	통과 (0.34ms, 31MB)
테스트 9 〉	통과 (0.20ms, 31.1MB)
테스트 10 〉	통과 (0.32ms, 31MB)
테스트 11 〉	통과 (0.21ms, 31.3MB)
테스트 12 〉	통과 (0.21ms, 30.9MB)
테스트 13 〉	통과 (0.21ms, 31.2MB)
테스트 14 〉	통과 (0.21ms, 31MB)
테스트 15 〉	통과 (0.20ms, 31.3MB)
테스트 16 〉	통과 (0.20ms, 31.3MB)
테스트 17 〉	통과 (0.20ms, 30.9MB)
테스트 18 〉	통과 (0.20ms, 31MB)
테스트 19 〉	통과 (0.20ms, 31.4MB)
테스트 20 〉	통과 (0.20ms, 31.2MB)
테스트 21 〉	통과 (0.32ms, 31.2MB)
테스트 22 〉	통과 (0.21ms, 31.2MB)
테스트 23 〉	통과 (0.21ms, 31.2MB)
테스트 24 〉	통과 (0.33ms, 31MB)
테스트 25 〉	통과 (0.21ms, 31MB)
```