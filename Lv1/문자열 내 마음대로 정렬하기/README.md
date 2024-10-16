# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12915">문자열 내 마음대로 정렬하기</a>

### 문제설명

문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 

예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.

***

### 제한사항

 - strings는 길이 1 이상, 50이하인 배열입니다.
 - strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
 - strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
 - 모든 strings의 원소의 길이는 n보다 큽니다.
 - 인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

***

### 답안
``` csharp
using System;

public class Word : IComparable<Word> {
    public char[] word;
    int index;
    public Word(char[] _word, int _index) {
        word = _word;
        index = _index;
    }
    int IComparable<Word>.CompareTo(Word _other) {
        int result = word[index] - _other.word[index];
        if(result == 0) {
            string str = new string(word);
            string other = new string(_other.word);
            result = str.CompareTo(other);
        }
        return result;
    }
}

public class Solution {
    public string[] solution(string[] strings, int n) {
        int length = strings.Length;
        string[] answer = new string[length];
        Word[] words = new Word[length];
        for(int i = 0; i < length; i++) {
            words[i] = new Word(strings[i].ToCharArray(), n);
        }
        Array.Sort(words);
        for(int i = 0; i < length; i++) {
            answer[i] = new string(words[i].word);
        }
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (1.27ms, 31.2MB)
테스트 2 〉	통과 (5.21ms, 31.7MB)
테스트 3 〉	통과 (3.98ms, 31.8MB)
테스트 4 〉	통과 (4.07ms, 31.7MB)
테스트 5 〉	통과 (4.14ms, 31.9MB)
테스트 6 〉	통과 (3.98ms, 31.8MB)
테스트 7 〉	통과 (3.95ms, 31.9MB)
테스트 8 〉	통과 (3.86ms, 31.6MB)
테스트 9 〉	통과 (5.03ms, 31.8MB)
테스트 10 〉	통과 (4.17ms, 32.1MB)
테스트 11 〉	통과 (3.99ms, 31.5MB)
```