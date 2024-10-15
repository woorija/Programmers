# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42748">K번째수</a>

### 문제설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

 1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
 2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
 3. 2에서 나온 배열의 3번째 숫자는 5입니다.

배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - array의 길이는 1 이상 100 이하입니다.
 - array의 각 원소는 1 이상 100 이하입니다.
 - commands의 길이는 1 이상 50 이하입니다.
 - commands의 각 원소는 길이가 3입니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int[] solution(int[] array, int[,] commands) {
        List<int> answer = new List<int>();
        
        for(int i = 0;i < commands.GetLength(0); i++) {
            int value = SliceAndSort(array, commands[i,0] - 1, commands[i,1] - 1, commands[i,2] - 1);
            answer.Add(value);
        }
        return answer.ToArray();
    }
    public int SliceAndSort(int[] _array, int _first, int _second, int _index){
        List<int> list = new List<int>();
        for(int i = _first; i <= _second; i++) {
            list.Add(_array[i]);
        }
        list.Sort();
        return list[_index];
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.94ms, 31.3MB)
테스트 2 〉	통과 (2.00ms, 31MB)
테스트 3 〉	통과 (1.93ms, 31.1MB)
테스트 4 〉	통과 (2.00ms, 31.3MB)
테스트 5 〉	통과 (2.04ms, 31MB)
테스트 6 〉	통과 (2.03ms, 31.1MB)
테스트 7 〉	통과 (1.90ms, 31.2MB)
```