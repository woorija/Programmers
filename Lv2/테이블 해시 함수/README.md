# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/147354">테이블 해시 함수</a>

### 문제설명

완호가 관리하는 어떤 데이터베이스의 한 테이블은 모두 정수 타입인 컬럼들로 이루어져 있습니다. 테이블은 2차원 행렬로 표현할 수 있으며 열은 컬럼을 나타내고, 행은 튜플을 나타냅니다.

첫 번째 컬럼은 기본키로서 모든 튜플에 대해 그 값이 중복되지 않도록 보장됩니다. 완호는 이 테이블에 대한 해시 함수를 다음과 같이 정의하였습니다.

 1. 해시 함수는 col, row_begin, row_end을 입력으로 받습니다.
 2. 테이블의 튜플을 col번째 컬럼의 값을 기준으로 오름차순 정렬을 하되, 만약 그 값이 동일하면 기본키인 첫 번째 컬럼의 값을 기준으로 내림차순 정렬합니다.
 3. 정렬된 데이터에서 S_i를 i 번째 행의 튜플에 대해 각 컬럼의 값을 i 로 나눈 나머지들의 합으로 정의합니다.
 4. row_begin ≤ i ≤ row_end 인 모든 S_i를 누적하여 bitwise XOR 한 값을 해시 값으로서 반환합니다.

테이블의 데이터 data와 해시 함수에 대한 입력 col, row_begin, row_end이 주어졌을 때 테이블의 해시 값을 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ data의 길이 ≤ 2,500
 - 1 ≤ data의 원소의 길이 ≤ 500
 - 1 ≤ data[i][j] ≤ 1,000,000
   - data[i][j]는 i + 1 번째 튜플의 j + 1 번째 컬럼의 값을 의미합니다.
 - 1 ≤ col ≤ data의 원소의 길이
 - 1 ≤ row_begin ≤ row_end ≤ data의 길이

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Tuple : IComparable<Tuple> {
    public int[] data;
    public int sortIndex;
    public Tuple(int[] _data, int _sortIndex){
        data = _data;
        sortIndex = _sortIndex-1;
    }
    int IComparable<Tuple>.CompareTo(Tuple _other) {
        int result = data[sortIndex] - _other.data[sortIndex];
        if(result == 0) {
            result = _other.data[0] - data[0];
        }
        return result;
    }
}

public class Solution {
    public int solution(int[,] data, int col, int row_begin, int row_end) {
        int answer = 0;
        int tupleLength = data.GetLength(1);
        List<Tuple> list = new List<Tuple>();
        
        for(int i = 0; i < data.GetLength(0); i++) {
            int[] tuple = new int[tupleLength];
            for(int j = 0; j < tupleLength; j++) {
                tuple[j] = data[i,j];
            }
            list.Add(new Tuple(tuple, col));
        }
        
        list.Sort();
        
        int[] S = new int[row_end - row_begin + 1];
        
        for(int i = 0; i < S.Length; i++) {
            int value = row_begin + i;
            int sum = 0;
            for(int j = 0; j < tupleLength; j++) {
                sum += list[value - 1].data[j] % value;
            }
            S[i] = sum;
        }
        answer = S[0];
        for(int i = 1; i < S.Length; i++) {
            answer = answer ^ S[i];
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.47ms, 31.2MB)
테스트 2 〉	통과 (1.52ms, 30.9MB)
테스트 3 〉	통과 (2.35ms, 31.3MB)
테스트 4 〉	통과 (1.48ms, 31.6MB)
테스트 5 〉	통과 (3.12ms, 32.2MB)
테스트 6 〉	통과 (13.97ms, 64.1MB)
테스트 7 〉	통과 (16.39ms, 64.2MB)
테스트 8 〉	통과 (19.07ms, 64.4MB)
테스트 9 〉	통과 (17.59ms, 64.1MB)
테스트 10 〉	통과 (17.13ms, 64MB)
테스트 11 〉	통과 (0.74ms, 31.4MB)
```