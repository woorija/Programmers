# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42842">카펫</a>

### 문제설명

Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
 - 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
 - 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int[] solution(int brown, int yellow) {
        int count = brown + yellow;
        int width = 0;
        int height = 0;
        int widthY;
        int heightY;
        for(int i = count / 2; i >= 3; i--) {
            if(count % i == 0) {
                width = count / i;
                height = count / width;
                widthY = width - 2;
                heightY = height - 2;
                if(widthY * heightY == yellow) {
                    break;
                }
            }
        }
        int[] answer = new int[] { height, width };
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.18ms, 31.3MB)
테스트 2 〉	통과 (0.18ms, 31.3MB)
테스트 3 〉	통과 (1.70ms, 31.1MB)
테스트 4 〉	통과 (0.20ms, 31.3MB)
테스트 5 〉	통과 (0.20ms, 31.4MB)
테스트 6 〉	통과 (0.71ms, 31.2MB)
테스트 7 〉	통과 (2.15ms, 31.2MB)
테스트 8 〉	통과 (1.70ms, 30.8MB)
테스트 9 〉	통과 (2.18ms, 31.3MB)
테스트 10 〉	통과 (2.45ms, 31.2MB)
테스트 11 〉	통과 (0.18ms, 31.3MB)
테스트 12 〉	통과 (0.19ms, 31.3MB)
테스트 13 〉	통과 (0.31ms, 31.4MB)
```