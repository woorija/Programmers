# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/135807">숫자 카드 나누기</a>

### 문제설명

철수와 영희는 선생님으로부터 숫자가 하나씩 적힌 카드들을 절반씩 나눠서 가진 후, 다음 두 조건 중 하나를 만족하는 가장 큰 양의 정수 a의 값을 구하려고 합니다.

 1. 철수가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고 영희가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a
 2. 영희가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고, 철수가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a

예를 들어, 카드들에 10, 5, 20, 17이 적혀 있는 경우에 대해 생각해 봅시다. 만약, 철수가 [10, 17]이 적힌 카드를 갖고, 영희가 [5, 20]이 적힌 카드를 갖는다면 두 조건 중 하나를 만족하는 양의 정수 a는 존재하지 않습니다. 하지만, 철수가 [10, 20]이 적힌 카드를 갖고, 영희가 [5, 17]이 적힌 카드를 갖는다면, 철수가 가진 카드들의 숫자는 모두 10으로 나눌 수 있고, 영희가 가진 카드들의 숫자는 모두 10으로 나눌 수 없습니다. 따라서 철수와 영희는 각각 [10, 20]이 적힌 카드, [5, 17]이 적힌 카드로 나눠 가졌다면 조건에 해당하는 양의 정수 a는 10이 됩니다.

철수가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 arrayA와 영희가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 arrayB가 주어졌을 때, 주어진 조건을 만족하는 가장 큰 양의 정수 a를 return하도록 solution 함수를 완성해 주세요. 만약, 조건을 만족하는 a가 없다면, 0을 return 해 주세요.

***

### 제한사항

 - 1 ≤ arrayA의 길이 = arrayB의 길이 ≤ 500,000
 - 1 ≤ arrayA의 원소, arrayB의 원소 ≤ 100,000,000
 - arrayA와 arrayB에는 중복된 원소가 있을 수 있습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int[] arrayA, int[] arrayB) {
        int answer = 0;
        int gdcA = arrayA[0];
        int gdcB = arrayB[0];
        int length = arrayA.Length;
        bool countA = false;
        bool countB = false;
        
        for(int i = 1; i < length; i++) {
            gdcA = gdc(gdcA, arrayA[i]);
            gdcB = gdc(gdcB, arrayB[i]);
        }
        
        for(int i = 0; i < length; i++) {
            if(arrayB[i] % gdcA == 0) {
                countA = true;
                break;
            }
        }
        for(int i = 0; i < length; i++) {
            if(arrayA[i] % gdcB == 0) {
                countB = true;
                break;
            }
        }
        
        if(countA && countB) {
            return 0;
        }else if(countA) {
            return gdcB;
        }else if(countB) {
            return gdcA;
        }else{
            return Math.Max(gdcA, gdcB);
        }
    }
    
    int gdc(int a, int b) {
        if(b == 0) {
            return a;
        }else{
            return gdc(b, a % b);
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.32ms, 31.5MB)
테스트 2 〉	통과 (0.38ms, 31.2MB)
테스트 3 〉	통과 (0.29ms, 31.1MB)
테스트 4 〉	통과 (1.43ms, 32.5MB)
테스트 5 〉	통과 (0.45ms, 31.4MB)
테스트 6 〉	통과 (0.67ms, 31.6MB)
테스트 7 〉	통과 (0.32ms, 31.2MB)
테스트 8 〉	통과 (0.31ms, 31.1MB)
테스트 9 〉	통과 (0.49ms, 31.3MB)
테스트 10 〉	통과 (0.30ms, 31.4MB)
테스트 11 〉	통과 (15.83ms, 50.3MB)
테스트 12 〉	통과 (15.62ms, 50MB)
테스트 13 〉	통과 (14.77ms, 50.1MB)
테스트 14 〉	통과 (14.69ms, 50.2MB)
테스트 15 〉	통과 (14.75ms, 50.1MB)
테스트 16 〉	통과 (14.69ms, 49.9MB)
테스트 17 〉	통과 (13.94ms, 50.2MB)
테스트 18 〉	통과 (14.71ms, 50MB)
테스트 19 〉	통과 (0.25ms, 31.2MB)
테스트 20 〉	통과 (0.29ms, 31.3MB)
테스트 21 〉	통과 (0.28ms, 31.3MB)
테스트 22 〉	통과 (0.30ms, 31.5MB)
테스트 23 〉	통과 (0.44ms, 31.7MB)
테스트 24 〉	통과 (0.30ms, 31.5MB)
테스트 25 〉	통과 (0.27ms, 31.2MB)
테스트 26 〉	통과 (0.27ms, 31.4MB)
테스트 27 〉	통과 (0.28ms, 31.5MB)
테스트 28 〉	통과 (0.28ms, 31.3MB)
테스트 29 〉	통과 (0.27ms, 31.1MB)
테스트 30 〉	통과 (0.25ms, 31.6MB)
테스트 31 〉	통과 (0.25ms, 31.5MB)
테스트 32 〉	통과 (0.27ms, 31.4MB)
테스트 33 〉	통과 (0.27ms, 31.5MB)
테스트 34 〉	통과 (0.27ms, 31.2MB)
테스트 35 〉	통과 (0.29ms, 31.3MB)
테스트 36 〉	통과 (0.29ms, 31.2MB)
```