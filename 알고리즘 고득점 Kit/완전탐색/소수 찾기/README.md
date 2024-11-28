# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42839">소수 찾기</a>

### 문제설명

한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - numbers는 길이 1 이상 7 이하인 문자열입니다.
 - numbers는 0~9까지 숫자만으로 이루어져 있습니다.
 - "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    List<int> numList;
    HashSet<int> numberSet;
    bool[] useIndex;
    int answer;
    int length;
    public int solution(string numbers) {
        answer = 0;
        length = numbers.Length;
        numberSet = new HashSet<int>();
        useIndex = new bool[numbers.Length];
        for(int i = 0; i < length; i++) {
            dfs(numbers, "", i);
        }
        numList = new List<int>(numberSet);
        
        for(int i = 0; i < numList.Count; i++) {
            if(IsPrime(numList[i])) {
                answer++;
            }
        }
        return answer;
    }
    void dfs(string _numbers, string _num, int _index) {
        if(useIndex[_index]) return;
        useIndex[_index] = true;
        string num = _num + _numbers[_index];
        numberSet.Add(int.Parse(num));
        for(int i = 0; i < length; i++) {
            dfs(_numbers, num.ToString(), i);
        }
        useIndex[_index] = false;
    }
    bool IsPrime(int _num) {
        if(_num == 0 || _num == 1) return false;
        if(_num == 2) return true;

        int sqrtNum = (int)Math.Sqrt(_num);
        for(int i = 2; i <= sqrtNum + 1; i++) {
            if(_num % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.13ms, 31.3MB)
테스트 2 〉	통과 (2.91ms, 31.5MB)
테스트 3 〉	통과 (2.07ms, 31.2MB)
테스트 4 〉	통과 (2.82ms, 31.5MB)
테스트 5 〉	통과 (6.23ms, 32.4MB)
테스트 6 〉	통과 (1.98ms, 31.3MB)
테스트 7 〉	통과 (2.22ms, 31.3MB)
테스트 8 〉	통과 (6.23ms, 32.5MB)
테스트 9 〉	통과 (2.10ms, 31.5MB)
테스트 10 〉	통과 (3.10ms, 31.8MB)
테스트 11 〉	통과 (2.29ms, 31.2MB)
```