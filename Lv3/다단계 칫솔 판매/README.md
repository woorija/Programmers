# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/77486">다단계 칫솔 판매</a>

### 문제설명

민호는 다단계 조직을 이용하여 칫솔을 판매하고 있습니다. 판매원이 칫솔을 판매하면 그 이익이 피라미드 조직을 타고 조금씩 분배되는 형태의 판매망입니다. 어느정도 판매가 이루어진 후, 조직을 운영하던 민호는 조직 내 누가 얼마만큼의 이득을 가져갔는지가 궁금해졌습니다.

민호는 center이며, 각각은 자신을 조직에 참여시킨 추천인에 연결되어 피라미드 식의 구조를 이루고 있습니다. 조직의 이익 분배 규칙은 간단합니다. 모든 판매원은 칫솔의 판매에 의하여 발생하는 이익에서 10% 를 계산하여 자신을 조직에 참여시킨 추천인에게 배분하고 나머지는 자신이 가집니다. 모든 판매원은 자신이 칫솔 판매에서 발생한 이익 뿐만 아니라, 자신이 조직에 추천하여 가입시킨 판매원에게서 발생하는 이익의 10% 까지 자신에 이익이 됩니다. 자신에게 발생하는 이익 또한 마찬가지의 규칙으로 자신의 추천인에게 분배됩니다. 단, 10% 를 계산할 때에는 원 단위에서 절사하며, 10%를 계산한 금액이 1 원 미만인 경우에는 이득을 분배하지 않고 자신이 모두 가집니다.

각 판매원의 이름을 담은 배열 enroll, 각 판매원을 다단계 조직에 참여시킨 다른 판매원의 이름을 담은 배열 referral, 판매량 집계 데이터의 판매원 이름을 나열한 배열 seller, 판매량 집계 데이터의 판매 수량을 나열한 배열 amount가 매개변수로 주어질 때, 각 판매원이 득한 이익금을 나열한 배열을 return 하도록 solution 함수를 완성해주세요. 판매원에게 배분된 이익금의 총합을 계산하여(정수형으로), 입력으로 주어진 enroll에 이름이 포함된 순서에 따라 나열하면 됩니다.

***

### 제한사항

 - enroll의 길이는 1 이상 10,000 이하입니다.
   - enroll에 민호의 이름은 없습니다. 따라서 enroll의 길이는 민호를 제외한 조직 구성원의 총 수입니다.
 - referral의 길이는 enroll의 길이와 같습니다.
   - referral 내에서 i 번째에 있는 이름은 배열 enroll 내에서 i 번째에 있는 판매원을 조직에 참여시킨 사람의 이름입니다.
   - 어느 누구의 추천도 없이 조직에 참여한 사람에 대해서는 referral 배열 내에 추천인의 이름이 기입되지 않고 “-“ 가 기입됩니다. 위 예제에서는 john 과 mary 가 이러한 예에 해당합니다.
   - enroll 에 등장하는 이름은 조직에 참여한 순서에 따릅니다.
   - 즉, 어느 판매원의 이름이 enroll 의 i 번째에 등장한다면, 이 판매원을 조직에 참여시킨 사람의 이름, 즉 referral 의 i 번째 원소는 이미 배열 enroll 의 j 번째 (j < i) 에 등장했음이 보장됩니다.
 - seller의 길이는 1 이상 100,000 이하입니다.
   - seller 내의 i 번째에 있는 이름은 i 번째 판매 집계 데이터가 어느 판매원에 의한 것인지를 나타냅니다.
   - seller 에는 같은 이름이 중복해서 들어있을 수 있습니다.
 - amount의 길이는 seller의 길이와 같습니다.
   - amount 내의 i 번째에 있는 수는 i 번째 판매 집계 데이터의 판매량을 나타냅니다.
   - 판매량의 범위, 즉 amount 의 원소들의 범위는 1 이상 100 이하인 자연수입니다.
 - 칫솔 한 개를 판매하여 얻어지는 이익은 100 원으로 정해져 있습니다.
 - 모든 조직 구성원들의 이름은 10 글자 이내의 영문 알파벳 소문자들로만 이루어져 있습니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Node {
    public int money;
    public Node parent;
    
    public void SetParent(Node _node) {
        parent = _node;
    }
    
    public void GetMoney(int _money) {
        if(_money == 0) return;
        int temp = (int)Math.Ceiling((double)_money * 9 / 10);
        money += temp;
        if(parent != null) {
            parent.GetMoney(_money - temp);
        }
    }
}

public class Solution {
    public int[] solution(string[] enroll, string[] referral, string[] seller, int[] amount) {
        int[] answer = new int[enroll.Length];
        Dictionary<string, Node> nodes = new Dictionary<string, Node>();
        
        for(int i = 0; i < enroll.Length; i++) {
            nodes.Add(enroll[i], new Node());
            if(referral[i] != "-") {
                nodes[enroll[i]].SetParent(nodes[referral[i]]);
            }
        }
        
        for(int i = 0; i < seller.Length; i++) {
            nodes[seller[i]].GetMoney(amount[i] * 100);
        }
        
        int index = 0;
        foreach(Node node in nodes.Values) {
            answer[index] = node.money;
            index++;
        }
        
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.27ms, 31.3MB)
테스트 2 〉	통과 (1.20ms, 31.4MB)
테스트 3 〉	통과 (1.23ms, 31.3MB)
테스트 4 〉	통과 (1.00ms, 31.2MB)
테스트 5 〉	통과 (1.38ms, 31.4MB)
테스트 6 〉	통과 (6.48ms, 35.6MB)
테스트 7 〉	통과 (4.16ms, 35.8MB)
테스트 8 〉	통과 (4.80ms, 36.2MB)
테스트 9 〉	통과 (6.34ms, 41.1MB)
테스트 10 〉	통과 (32.36ms, 57.9MB)
테스트 11 〉	통과 (25.21ms, 57.6MB)
테스트 12 〉	통과 (24.29ms, 57.8MB)
```