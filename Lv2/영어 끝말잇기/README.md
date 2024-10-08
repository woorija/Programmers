# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12981">영어 끝말잇기</a>

### 문제설명

1부터 n까지 번호가 붙어있는 n명의 사람이 영어 끝말잇기를 하고 있습니다. 영어 끝말잇기는 다음과 같은 규칙으로 진행됩니다.

 1. 1번부터 번호 순서대로 한 사람씩 차례대로 단어를 말합니다.
 2. 마지막 사람이 단어를 말한 다음에는 다시 1번부터 시작합니다.
 3. 앞사람이 말한 단어의 마지막 문자로 시작하는 단어를 말해야 합니다.
 4. 이전에 등장했던 단어는 사용할 수 없습니다.
 5. 한 글자인 단어는 인정되지 않습니다.
다음은 3명이 끝말잇기를 하는 상황을 나타냅니다.

tank → kick → know → wheel → land → dream → mother → robot → tank

위 끝말잇기는 다음과 같이 진행됩니다.

 - 1번 사람이 자신의 첫 번째 차례에 tank를 말합니다.
 - 2번 사람이 자신의 첫 번째 차례에 kick을 말합니다.
 - 3번 사람이 자신의 첫 번째 차례에 know를 말합니다.
 - 1번 사람이 자신의 두 번째 차례에 wheel을 말합니다.
 - (계속 진행)
끝말잇기를 계속 진행해 나가다 보면, 3번 사람이 자신의 세 번째 차례에 말한 tank 라는 단어는 이전에 등장했던 단어이므로 탈락하게 됩니다.

사람의 수 n과 사람들이 순서대로 말한 단어 words 가 매개변수로 주어질 때, 가장 먼저 탈락하는 사람의 번호와 그 사람이 자신의 몇 번째 차례에 탈락하는지를 구해서 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 끝말잇기에 참여하는 사람의 수 n은 2 이상 10 이하의 자연수입니다.
 - words는 끝말잇기에 사용한 단어들이 순서대로 들어있는 배열이며, 길이는 n 이상 100 이하입니다.
 - 단어의 길이는 2 이상 50 이하입니다.
 - 모든 단어는 알파벳 소문자로만 이루어져 있습니다.
 - 끝말잇기에 사용되는 단어의 뜻(의미)은 신경 쓰지 않으셔도 됩니다.
 - 정답은 [ 번호, 차례 ] 형태로 return 해주세요.
 - 만약 주어진 단어들로 탈락자가 생기지 않는다면, [0, 0]을 return 해주세요.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

class Solution
{
    public int[] solution(int n, string[] words)
    {
        Dictionary<string,bool> dic = new Dictionary<string,bool>(words.Length);
        int[] answer = new int[2];
        dic.Add(words[0], true);
        for(int i = 1; i < words.Length; i++) {
            if(dic.ContainsKey(words[i])){
                answer[0] = i%n +1;
                answer[1] = i/n+1;
                break;
            }else if(words[i-1][words[i-1].Length-1] != words[i][0]){
                answer[0] = i % n + 1;
                answer[1] = i / n + 1;
                break;
            }
            else{
                dic.Add(words[i], true);
            }
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.33ms, 31.4MB)
테스트 2 〉	통과 (1.33ms, 31.3MB)
테스트 3 〉	통과 (1.34ms, 31.3MB)
테스트 4 〉	통과 (1.40ms, 31.1MB)
테스트 5 〉	통과 (1.33ms, 31.3MB)
테스트 6 〉	통과 (1.36ms, 31.1MB)
테스트 7 〉	통과 (1.41ms, 31.5MB)
테스트 8 〉	통과 (1.33ms, 31.1MB)
테스트 9 〉	통과 (1.33ms, 31.5MB)
테스트 10 〉	통과 (1.33ms, 31.2MB)
테스트 11 〉	통과 (1.40ms, 31.1MB)
테스트 12 〉	통과 (1.38ms, 31.4MB)
테스트 13 〉	통과 (1.33ms, 31.2MB)
테스트 14 〉	통과 (1.34ms, 31.3MB)
테스트 15 〉	통과 (1.36ms, 31.3MB)
테스트 16 〉	통과 (1.35ms, 31MB)
테스트 17 〉	통과 (1.49ms, 31MB)
테스트 18 〉	통과 (1.40ms, 31.2MB)
테스트 19 〉	통과 (1.40ms, 31.6MB)
테스트 20 〉	통과 (1.43ms, 30.9MB)
```