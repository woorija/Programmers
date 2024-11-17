# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/92342">양궁대회</a>

### 문제설명

카카오배 양궁대회가 열렸습니다.

라이언은 저번 카카오배 양궁대회 우승자이고 이번 대회에도 결승전까지 올라왔습니다. 결승전 상대는 어피치입니다.

카카오배 양궁대회 운영위원회는 한 선수의 연속 우승보다는 다양한 선수들이 양궁대회에서 우승하기를 원합니다. 따라서, 양궁대회 운영위원회는 결승전 규칙을 전 대회 우승자인 라이언에게 불리하게 다음과 같이 정했습니다.

 1. 어피치가 화살 n발을 다 쏜 후에 라이언이 화살 n발을 쏩니다.
 2. 점수를 계산합니다.
   1. 가장 작은 원의 과녁 점수는 10점이고 가장 큰 원의 바깥쪽은 과녁 점수가 0점입니다.
   2. 만약, k(k는 1~10사이의 자연수)점을 어피치가 a발을 맞혔고 라이언이 b발을 맞혔을 경우 더 많은 화살을 k점에 맞힌 선수가 k 점을 가져갑니다. 단, a = b일 경우는 어피치가 k점을 가져갑니다. k점을 여러 발 맞혀도 k점 보다 많은 점수를 가져가는 게 아니고 k점만 가져가는 것을 유의하세요. 또한 a = b = 0 인 경우, 즉, 라이언과 어피치 모두 k점에 단 하나의 화살도 맞히지 못한 경우는 어느 누구도 k점을 가져가지 않습니다.
     - 예를 들어, 어피치가 10점을 2발 맞혔고 라이언도 10점을 2발 맞혔을 경우 어피치가 10점을 가져갑니다.
     - 다른 예로, 어피치가 10점을 0발 맞혔고 라이언이 10점을 2발 맞혔을 경우 라이언이 10점을 가져갑니다.
   3. 모든 과녁 점수에 대하여 각 선수의 최종 점수를 계산합니다.
 3. 최종 점수가 더 높은 선수를 우승자로 결정합니다. 단, 최종 점수가 같을 경우 어피치를 우승자로 결정합니다.

현재 상황은 어피치가 화살 n발을 다 쏜 후이고 라이언이 화살을 쏠 차례입니다.

라이언은 어피치를 가장 큰 점수 차이로 이기기 위해서 n발의 화살을 어떤 과녁 점수에 맞혀야 하는지를 구하려고 합니다.

화살의 개수를 담은 자연수 n, 어피치가 맞힌 과녁 점수의 개수를 10점부터 0점까지 순서대로 담은 정수 배열 info가 매개변수로 주어집니다. 이때, 라이언이 가장 큰 점수 차이로 우승하기 위해 n발의 화살을 어떤 과녁 점수에 맞혀야 하는지를 10점부터 0점까지 순서대로 정수 배열에 담아 return 하도록 solution 함수를 완성해 주세요. 만약, 라이언이 우승할 수 없는 경우(무조건 지거나 비기는 경우)는 [-1]을 return 해주세요.

***

### 제한사항

 - 1 ≤ n ≤ 10
 - info의 길이 = 11
   - 0 ≤ info의 원소 ≤ n
   - info의 원소 총합 = n
   - info의 i번째 원소는 과녁의 10 - i 점을 맞힌 화살 개수입니다. ( i는 0~10 사이의 정수입니다.)
 - 라이언이 우승할 방법이 있는 경우, return 할 정수 배열의 길이는 11입니다.
   - 0 ≤ return할 정수 배열의 원소 ≤ n
   - return할 정수 배열의 원소 총합 = n (꼭 n발을 다 쏴야 합니다.)
   - return할 정수 배열의 i번째 원소는 과녁의 10 - i 점을 맞힌 화살 개수입니다. ( i는 0~10 사이의 정수입니다.)
   - 라이언이 가장 큰 점수 차이로 우승할 수 있는 방법이 여러 가지 일 경우, 가장 낮은 점수를 더 많이 맞힌 경우를 return 해주세요.
     - 가장 낮은 점수를 맞힌 개수가 같을 경우 계속해서 그다음으로 낮은 점수를 더 많이 맞힌 경우를 return 해주세요.
     - 예를 들어, [2,3,1,0,0,0,0,1,3,0,0]과 [2,1,0,2,0,0,0,2,3,0,0]를 비교하면 [2,1,0,2,0,0,0,2,3,0,0]를 return 해야 합니다.
     - 다른 예로, [0,0,2,3,4,1,0,0,0,0,0]과 [9,0,0,0,0,0,0,0,1,0,0]를 비교하면[9,0,0,0,0,0,0,0,1,0,0]를 return 해야 합니다.
 - 라이언이 우승할 방법이 없는 경우, return 할 정수 배열의 길이는 1입니다.
   - 라이언이 어떻게 화살을 쏘든 라이언의 점수가 어피치의 점수보다 낮거나 같으면 [-1]을 return 해야 합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class AnswerArray : IComparable<AnswerArray> {
    public int[] arr;
    
    public AnswerArray(int[] _arr) {
        arr = _arr;
    }
    
    int IComparable<AnswerArray>.CompareTo(AnswerArray _other) {
        int result = 0;
        for(int i = 10; i >= 0; i--) {
            result = _other.arr[i] - arr[i];
            if(result != 0) {
                return result;
            }
        }
        return 0;
    }
}

public class Solution {
    int[] temp;
    int[] scores;
    int score;
    List<AnswerArray> answerList;
    
    public int[] solution(int n, int[] info) {
        temp = new int[11];
        scores = info;
        score = -1;
        answerList = new List<AnswerArray>();
        
        if(n >= info[0] + 1) {
            dfs(0, info[0] + 1, n - (info[0] + 1));
            temp[0] = 0;
        }
        dfs(0, 0, n);
        
        if(score == -1) {
            return new int[1] { -1 };
        }
        
        answerList.Sort();
        
        return answerList[0].arr;
    }
    
    void dfs(int _index, int _count, int _remaining) {
        temp[_index] = _count;

        if(_index == 10) {
            temp[_index] += _remaining;
            int tempScore = 0;
            
            for(int i = 0; i <= 10; i++) {
                if(scores[i] > temp[i]) {
                    tempScore -= 10 - i;
                }else if(scores[i] < temp[i]) {
                    tempScore += 10 - i;
                }
            }
            
            if(tempScore > 0 && score <= tempScore) {
                if(score < tempScore) {
                    answerList.Clear();
                    score = tempScore;
                }
                
                int[] arr = new int[11];
                
                for(int i = 0; i < 11; i++) {
                    arr[i] = temp[i];
                }
                
                answerList.Add(new AnswerArray(arr));
            }
            return;
        }

        if(_remaining >= scores[_index + 1] + 1) {
            dfs(_index + 1, scores[_index + 1] + 1, _remaining - (scores[_index + 1] + 1));
            temp[_index + 1] = 0;
        }
        dfs(_index + 1, 0, _remaining);
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.85ms, 31.4MB)
테스트 2 〉	통과 (0.90ms, 30.8MB)
테스트 3 〉	통과 (0.91ms, 31.3MB)
테스트 4 〉	통과 (0.84ms, 31.3MB)
테스트 5 〉	통과 (0.84ms, 31MB)
테스트 6 〉	통과 (0.88ms, 31.1MB)
테스트 7 〉	통과 (0.83ms, 31.1MB)
테스트 8 〉	통과 (1.43ms, 31MB)
테스트 9 〉	통과 (1.31ms, 31MB)
테스트 10 〉	통과 (0.88ms, 31.5MB)
테스트 11 〉	통과 (0.78ms, 31.1MB)
테스트 12 〉	통과 (0.82ms, 31.3MB)
테스트 13 〉	통과 (0.86ms, 31.1MB)
테스트 14 〉	통과 (0.84ms, 31.4MB)
테스트 15 〉	통과 (0.91ms, 31MB)
테스트 16 〉	통과 (0.93ms, 31.1MB)
테스트 17 〉	통과 (0.80ms, 31.3MB)
테스트 18 〉	통과 (1.40ms, 31.3MB)
테스트 19 〉	통과 (0.64ms, 31.1MB)
테스트 20 〉	통과 (1.59ms, 31.2MB)
테스트 21 〉	통과 (1.60ms, 30.9MB)
테스트 22 〉	통과 (2.13ms, 31.2MB)
테스트 23 〉	통과 (0.63ms, 31.1MB)
테스트 24 〉	통과 (0.82ms, 31.2MB)
테스트 25 〉	통과 (0.93ms, 31.1MB)
```