# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/132265">롤케이크 자르기</a>

### 문제설명

철수는 롤케이크를 두 조각으로 잘라서 동생과 한 조각씩 나눠 먹으려고 합니다. 이 롤케이크에는 여러가지 토핑들이 일렬로 올려져 있습니다. 철수와 동생은 롤케이크를 공평하게 나눠먹으려 하는데, 그들은 롤케이크의 크기보다 롤케이크 위에 올려진 토핑들의 종류에 더 관심이 많습니다. 그래서 잘린 조각들의 크기와 올려진 토핑의 개수에 상관없이 각 조각에 동일한 가짓수의 토핑이 올라가면 공평하게 롤케이크가 나누어진 것으로 생각합니다.

예를 들어, 롤케이크에 4가지 종류의 토핑이 올려져 있다고 합시다. 토핑들을 1, 2, 3, 4와 같이 번호로 표시했을 때, 케이크 위에 토핑들이 [1, 2, 1, 3, 1, 4, 1, 2] 순서로 올려져 있습니다. 만약 세 번째 토핑(1)과 네 번째 토핑(3) 사이를 자르면 롤케이크의 토핑은 [1, 2, 1], [3, 1, 4, 1, 2]로 나뉘게 됩니다. 철수가 [1, 2, 1]이 놓인 조각을, 동생이 [3, 1, 4, 1, 2]가 놓인 조각을 먹게 되면 철수는 두 가지 토핑(1, 2)을 맛볼 수 있지만, 동생은 네 가지 토핑(1, 2, 3, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것이 아닙니다. 만약 롤케이크의 네 번째 토핑(3)과 다섯 번째 토핑(1) 사이를 자르면 [1, 2, 1, 3], [1, 4, 1, 2]로 나뉘게 됩니다. 이 경우 철수는 세 가지 토핑(1, 2, 3)을, 동생도 세 가지 토핑(1, 2, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것입니다. 공평하게 롤케이크를 자르는 방법은 여러가지 일 수 있습니다. 위의 롤케이크를 [1, 2, 1, 3, 1], [4, 1, 2]으로 잘라도 공평하게 나뉩니다. 어떤 경우에는 롤케이크를 공평하게 나누지 못할 수도 있습니다.

롤케이크에 올려진 토핑들의 번호를 저장한 정수 배열 topping이 매개변수로 주어질 때, 롤케이크를 공평하게 자르는 방법의 수를 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - 1 ≤ topping의 길이 ≤ 1,000,000
   - 1 ≤ topping의 원소 ≤ 10,000

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int[] topping) {
        int answer = 0;
        Dictionary<int,int> toppings = new Dictionary<int,int>();
        Dictionary<int,int> otherToppings = new Dictionary<int,int>();
        for(int i = 0; i < topping.Length; i++) {
            if(toppings.ContainsKey(topping[i])) {
                toppings[topping[i]]++;
            }else{
                toppings.Add(topping[i], 1);
            }
        }
        for(int i = 0; i < topping.Length; i++) {
            int temp = topping[i];
            toppings[temp]--;
            if(otherToppings.ContainsKey(temp)) {
                otherToppings[temp]++;
            }else{
                otherToppings.Add(temp, 1);
            }
            if(toppings[temp] == 0) {
                toppings.Remove(temp);
            }
            if(toppings.Count == otherToppings.Count) {
                answer++;
            }
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (3.62ms, 31.3MB)
테스트 2 〉	통과 (21.80ms, 34MB)
테스트 3 〉	통과 (15.49ms, 32.7MB)
테스트 4 〉	통과 (20.62ms, 32.5MB)
테스트 5 〉	통과 (149.87ms, 49.8MB)
테스트 6 〉	통과 (209.08ms, 51.3MB)
테스트 7 〉	통과 (172.54ms, 51.1MB)
테스트 8 〉	통과 (194.78ms, 51.1MB)
테스트 9 〉	통과 (204.23ms, 51.1MB)
테스트 10 〉	통과 (156.00ms, 51.1MB)
테스트 11 〉	통과 (16.54ms, 32.5MB)
테스트 12 〉	통과 (4.41ms, 32.3MB)
테스트 13 〉	통과 (161.46ms, 51MB)
테스트 14 〉	통과 (158.68ms, 50.2MB)
테스트 15 〉	통과 (172.35ms, 50.2MB)
테스트 16 〉	통과 (179.31ms, 50.3MB)
테스트 17 〉	통과 (168.05ms, 50MB)
테스트 18 〉	통과 (155.58ms, 50.3MB)
테스트 19 〉	통과 (169.79ms, 50.3MB)
테스트 20 〉	통과 (172.76ms, 50.3MB)
```