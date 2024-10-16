# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12977">소수 만들기</a>

### 문제설명

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
 - nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

***

### 답안
``` csharp
using System;

class Solution
{
    public int solution(int[] nums)
    {
        int answer = 0;
        int length = nums.Length;
        
        Array.Sort(nums);
        
        int max = nums[length - 1] + nums[length - 2] + nums[length - 3];
        bool[] isPrime = new bool[max + 1];
        
        for(int i = 2; i < isPrime.Length; i++) {
            isPrime[i] = true;
        }
        
        for(int i = 2; i <= Math.Sqrt(max); i++) {
            if(isPrime[i]) {
                int j = 2;
                while(i * j <= max) {
                    isPrime[i * j] = false;
                    j++;
                }
            }
        }
        
        for(int i = 0; i < length - 2; i++) {
            for(int j = i + 1; j < length - 1; j++) {
                for(int k = j + 1; k < length; k++) {
                    int temp = nums[i] + nums[j] + nums[k];
                    if(isPrime[temp]) {
                        answer++;
                    }
                }
            }
        }

        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.71ms, 31.6MB)
테스트 2 〉	통과 (2.41ms, 31.5MB)
테스트 3 〉	통과 (1.67ms, 31.4MB)
테스트 4 〉	통과 (1.68ms, 31.6MB)
테스트 5 〉	통과 (1.68ms, 31.1MB)
테스트 6 〉	통과 (2.85ms, 31.4MB)
테스트 7 〉	통과 (1.62ms, 31.4MB)
테스트 8 〉	통과 (1.87ms, 31.2MB)
테스트 9 〉	통과 (1.77ms, 31.4MB)
테스트 10 〉	통과 (2.32ms, 31.3MB)
테스트 11 〉	통과 (2.03ms, 31.1MB)
테스트 12 〉	통과 (1.65ms, 31.7MB)
테스트 13 〉	통과 (2.42ms, 31.6MB)
테스트 14 〉	통과 (1.82ms, 31.6MB)
테스트 15 〉	통과 (1.62ms, 31.3MB)
테스트 16 〉	통과 (2.60ms, 31.4MB)
테스트 17 〉	통과 (1.82ms, 31.3MB)
테스트 18 〉	통과 (1.51ms, 31.4MB)
테스트 19 〉	통과 (1.55ms, 31.4MB)
테스트 20 〉	통과 (1.93ms, 31.5MB)
테스트 21 〉	통과 (2.76ms, 31.3MB)
테스트 22 〉	통과 (1.76ms, 31.5MB)
테스트 23 〉	통과 (1.86ms, 31.6MB)
테스트 24 〉	통과 (2.25ms, 31.3MB)
테스트 25 〉	통과 (1.82ms, 31.4MB)
테스트 26 〉	통과 (1.53ms, 31.6MB)
```