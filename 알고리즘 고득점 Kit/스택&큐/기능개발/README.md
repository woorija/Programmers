# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42586">기능개발</a>

### 문제설명

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

***

### 제한사항

 - 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
 - 작업 진도는 100 미만의 자연수입니다.
 - 작업 속도는 100 이하의 자연수입니다.
 - 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int[] progresses, int[] speeds)
    {
        List<int> complete = new List<int>();
        for(int i = 0; i < progresses.Length; i++)
        {
            int value = (int)Math.Ceiling((100 - progresses[i]) / (float)speeds[i]);
            complete.Add(value);
        }
        List<int> answer = new List<int>();
        int count = 0;
        int day = complete[0];
        for(int i=0; i<complete.Count; i++) {
            if(day < complete[i]){
                answer.Add(count);
                count=1;
                day = complete[i];
            }else{
                count++;
            }
        }
        if(count != 0){
        answer.Add(count);
        }
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.79ms, 31.3MB)
테스트 2 〉	통과 (1.03ms, 31.1MB)
테스트 3 〉	통과 (0.77ms, 31.1MB)
테스트 4 〉	통과 (0.78ms, 31MB)
테스트 5 〉	통과 (0.89ms, 31.2MB)
테스트 6 〉	통과 (1.25ms, 31.1MB)
테스트 7 〉	통과 (0.83ms, 30.9MB)
테스트 8 〉	통과 (0.82ms, 31.2MB)
테스트 9 〉	통과 (1.00ms, 31.2MB)
테스트 10 〉	통과 (0.89ms, 31MB)
테스트 11 〉	통과 (0.84ms, 31.1MB)
```