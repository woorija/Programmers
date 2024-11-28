# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/43163">단어 변환</a>

### 문제설명

두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

 1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
 2. words에 있는 단어로만 변환할 수 있습니다.

예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

***

### 제한사항

 - 각 단어는 알파벳 소문자로만 이루어져 있습니다.
 - 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
 - words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
 - begin과 target은 같지 않습니다.
 - 변환할 수 없는 경우에는 0를 return 합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Counter{
    public string str;
    public int count;
    public Counter(string _str, int _count){
        str = _str;
        count = _count;
    }
}
public class Solution {
    public int solution(string begin, string target, string[] words) {
        if(!Array.Exists(words, str => str.Equals(target))) {
            return 0;
        }
        
        int answer = 0;
        HashSet<string> hash = new HashSet<string>();
        Queue<Counter> queue = new Queue<Counter>();
        queue.Enqueue(new Counter(begin, 0));
        
        while(queue.Count != 0) {
            Counter counter = queue.Dequeue();
            string word = counter.str;
            int count = counter.count;
            if(word.Equals(target)) {
                answer = count;
                break;
            }
            for(int i = 0; i < words.Length; i++) {
                if(hash.Contains(words[i])) continue;
                string nextWord = StringCount(word, words[i]);
                if(nextWord != "") {
                    queue.Enqueue(new Counter(nextWord, count + 1));
                }
            }
        }
        return answer;
    }
    string StringCount(string _str, string _word) {
        int count = 0;
        for(int i = 0; i < _str.Length; i++) {
            if(_str[i] != _word[i]) {
                count++;
                if(count > 1) {
                    break;
                }
            }
        }
        if(count == 1) {
            return _word;
        }
        return "";
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.03ms, 31.4MB)
테스트 2 〉	통과 (1.03ms, 31.1MB)
테스트 3 〉	통과 (1.16ms, 31.5MB)
테스트 4 〉	통과 (1.10ms, 31.3MB)
테스트 5 〉	통과 (0.61ms, 31.5MB)
```