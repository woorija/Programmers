# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/49993">스킬트리</a>

### 문제설명

선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

***

### 제한사항

 - 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
 - 스킬 순서와 스킬트리는 문자열로 표기합니다.
   - 예를 들어, C → B → D 라면 "CBD"로 표기합니다
 - 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
 - skill_trees는 길이 1 이상 20 이하인 배열입니다.
 - skill_trees의 원소는 스킬을 나타내는 문자열입니다.
   - skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string skill, string[] skill_trees) {
        int answer = 0;
        for(int i = 0; i < skill_trees.Length; i++) {
            bool check = true;
            string currentSkillTree = skill_trees[i];
            for(int j = currentSkillTree.Length - 1; j >= 0; j--) {
                if(skill.IndexOf(currentSkillTree[j]) == -1) {
                    currentSkillTree = currentSkillTree.Remove(j, 1);
                }
            }
            for(int j = skill.Length - 1; j >= 0; j--) {
                if(currentSkillTree.IndexOf(skill[j]) != -1 && currentSkillTree.IndexOf(skill[j]) < j) {
                    check = false;
                    break;
                }
            }
            if(check){
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
테스트 1 〉	통과 (0.30ms, 31.3MB)
테스트 2 〉	통과 (0.31ms, 31.2MB)
테스트 3 〉	통과 (0.31ms, 31.2MB)
테스트 4 〉	통과 (0.29ms, 30.9MB)
테스트 5 〉	통과 (0.28ms, 31.5MB)
테스트 6 〉	통과 (0.29ms, 31.1MB)
테스트 7 〉	통과 (0.28ms, 31.1MB)
테스트 8 〉	통과 (0.31ms, 31.5MB)
테스트 9 〉	통과 (0.32ms, 31.3MB)
테스트 10 〉	통과 (0.30ms, 31.3MB)
테스트 11 〉	통과 (0.28ms, 31MB)
테스트 12 〉	통과 (0.28ms, 31.2MB)
테스트 13 〉	통과 (0.32ms, 31.3MB)
테스트 14 〉	통과 (0.28ms, 31.4MB)
```