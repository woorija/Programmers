# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/131127">할인 행사</a>

### 문제설명

XYZ 마트는 일정한 금액을 지불하면 10일 동안 회원 자격을 부여합니다. XYZ 마트에서는 회원을 대상으로 매일 한 가지 제품을 할인하는 행사를 합니다. 할인하는 제품은 하루에 하나씩만 구매할 수 있습니다. 알뜰한 정현이는 자신이 원하는 제품과 수량이 할인하는 날짜와 10일 연속으로 일치할 경우에 맞춰서 회원가입을 하려 합니다.

예를 들어, 정현이가 원하는 제품이 바나나 3개, 사과 2개, 쌀 2개, 돼지고기 2개, 냄비 1개이며, XYZ 마트에서 14일간 회원을 대상으로 할인하는 제품이 날짜 순서대로 치킨, 사과, 사과, 바나나, 쌀, 사과, 돼지고기, 바나나, 돼지고기, 쌀, 냄비, 바나나, 사과, 바나나인 경우에 대해 알아봅시다. 첫째 날부터 열흘 간에는 냄비가 할인하지 않기 때문에 첫째 날에는 회원가입을 하지 않습니다. 둘째 날부터 열흘 간에는 바나나를 원하는 만큼 할인구매할 수 없기 때문에 둘째 날에도 회원가입을 하지 않습니다. 셋째 날, 넷째 날, 다섯째 날부터 각각 열흘은 원하는 제품과 수량이 일치하기 때문에 셋 중 하루에 회원가입을 하려 합니다.

정현이가 원하는 제품을 나타내는 문자열 배열 want와 정현이가 원하는 제품의 수량을 나타내는 정수 배열 number, XYZ 마트에서 할인하는 제품을 나타내는 문자열 배열 discount가 주어졌을 때, 회원등록시 정현이가 원하는 제품을 모두 할인 받을 수 있는 회원등록 날짜의 총 일수를 return 하는 solution 함수를 완성하시오. 가능한 날이 없으면 0을 return 합니다.

***

### 제한사항

 - 1 ≤ want의 길이 = number의 길이 ≤ 10
   - 1 ≤ number의 원소 ≤ 10
   - number[i]는 want[i]의 수량을 의미하며, number의 원소의 합은 10입니다.
 - 10 ≤ discount의 길이 ≤ 100,000
 - want와 discount의 원소들은 알파벳 소문자로 이루어진 문자열입니다.
   - 1 ≤ want의 원소의 길이, discount의 원소의 길이 ≤ 12

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    int answer = 0;
    Dictionary<string,int> counter = new Dictionary<string,int>();
    Dictionary<string,int> answerCounter = new Dictionary<string,int>();
    public int solution(string[] want, int[] number, string[] discount) {
        for(int i = 0; i < want.Length; i++) {
            counter.Add(want[i], number[i]);
        }
        for(int i = 0; i < 10; i++) {
            if(!answerCounter.ContainsKey(discount[i])) {
                answerCounter.Add(discount[i],1);
            }else{
                answerCounter[discount[i]]++;
            }
        }
        Check(want);
        for(int i = 10; i < discount.Length; i++) {
            Change(discount[i - 10], discount[i]);
            Check(want);
        }
        return answer;
    }
    void Check(string[] keys) {
        for(int i = 0; i < keys.Length; i++) {
            if(!answerCounter.ContainsKey(keys[i])) {
                return;
            }else if(answerCounter[keys[i]] != counter[keys[i]]) {
                return;
            }
        }
        answer++;
    }
    void Change(string prevKey, string nextKey) {
        answerCounter[prevKey]--;
        if(!answerCounter.ContainsKey(nextKey)) {
            answerCounter.Add(nextKey,1);
        }else{
            answerCounter[nextKey]++;
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (6.79ms, 32.7MB)
테스트 2 〉	통과 (38.99ms, 40.3MB)
테스트 3 〉	통과 (8.49ms, 33MB)
테스트 4 〉	통과 (35.10ms, 44.7MB)
테스트 5 〉	통과 (22.65ms, 39.6MB)
테스트 6 〉	통과 (5.30ms, 32.1MB)
테스트 7 〉	통과 (13.81ms, 33.6MB)
테스트 8 〉	통과 (50.93ms, 49.3MB)
테스트 9 〉	통과 (8.80ms, 33.1MB)
테스트 10 〉	통과 (25.32ms, 40.1MB)
테스트 11 〉	통과 (6.06ms, 32.2MB)
테스트 12 〉	통과 (1.46ms, 31.3MB)
```