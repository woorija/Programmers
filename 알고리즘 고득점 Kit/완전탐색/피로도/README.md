# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/87946">피로도</a>

### 문제설명

XX게임에는 피로도 시스템(0 이상의 정수로 표현합니다)이 있으며, 일정 피로도를 사용해서 던전을 탐험할 수 있습니다. 이때, 각 던전마다 탐험을 시작하기 위해 필요한 "최소 필요 피로도"와 던전 탐험을 마쳤을 때 소모되는 "소모 피로도"가 있습니다. "최소 필요 피로도"는 해당 던전을 탐험하기 위해 가지고 있어야 하는 최소한의 피로도를 나타내며, "소모 피로도"는 던전을 탐험한 후 소모되는 피로도를 나타냅니다. 예를 들어 "최소 필요 피로도"가 80, "소모 피로도"가 20인 던전을 탐험하기 위해서는 유저의 현재 남은 피로도는 80 이상 이어야 하며, 던전을 탐험한 후에는 피로도 20이 소모됩니다.

이 게임에는 하루에 한 번씩 탐험할 수 있는 던전이 여러개 있는데, 한 유저가 오늘 이 던전들을 최대한 많이 탐험하려 합니다. 유저의 현재 피로도 k와 각 던전별 "최소 필요 피로도", "소모 피로도"가 담긴 2차원 배열 dungeons 가 매개변수로 주어질 때, 유저가 탐험할수 있는 최대 던전 수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - k는 1 이상 5,000 이하인 자연수입니다.
 - dungeons의 세로(행) 길이(즉, 던전의 개수)는 1 이상 8 이하입니다.
   - dungeons의 가로(열) 길이는 2 입니다.
   - dungeons의 각 행은 각 던전의 ["최소 필요 피로도", "소모 피로도"] 입니다.
   - "최소 필요 피로도"는 항상 "소모 피로도"보다 크거나 같습니다.
   - "최소 필요 피로도"와 "소모 피로도"는 1 이상 1,000 이하인 자연수입니다.
   - 서로 다른 던전의 ["최소 필요 피로도", "소모 피로도"]가 서로 같을 수 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    int answer = 0;
    bool[] visit;
    public int solution(int k, int[,] dungeons) {
        visit = new bool[dungeons.Length/2];
        for(int i = 0; i < dungeons.Length / 2; i++) {
            dfs(k, dungeons, i, 0);
        }
        return answer;
    }
    void dfs(int k, int[,] dungeons, int index, int result){
        if(visit[index]) return;
        if(k < dungeons[index,0]) {
            visit[index] = true;
        }else{
            k-=dungeons[index,1];
            visit[index] = true;
            result++;
            if(result > answer) {
                answer = result;
            }
        }
        for(int i = 0; i < dungeons.Length / 2; i++) {
            dfs(k, dungeons, i, result);
        }
        visit[index] = false;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.35ms, 31.4MB)
테스트 2 〉	통과 (0.29ms, 31.3MB)
테스트 3 〉	통과 (0.28ms, 31.4MB)
테스트 4 〉	통과 (0.28ms, 31.5MB)
테스트 5 〉	통과 (0.36ms, 31.4MB)
테스트 6 〉	통과 (0.81ms, 31MB)
테스트 7 〉	통과 (5.16ms, 31.4MB)
테스트 8 〉	통과 (5.19ms, 31.5MB)
테스트 9 〉	통과 (0.29ms, 31MB)
테스트 10 〉	통과 (0.87ms, 31.3MB)
테스트 11 〉	통과 (0.30ms, 31MB)
테스트 12 〉	통과 (5.03ms, 31.4MB)
테스트 13 〉	통과 (5.14ms, 31.5MB)
테스트 14 〉	통과 (8.15ms, 31.5MB)
테스트 15 〉	통과 (4.79ms, 31.4MB)
테스트 16 〉	통과 (0.81ms, 31.5MB)
테스트 17 〉	통과 (5.23ms, 31.5MB)
테스트 18 〉	통과 (0.40ms, 31.2MB)
테스트 19 〉	통과 (0.29ms, 31.4MB)
```