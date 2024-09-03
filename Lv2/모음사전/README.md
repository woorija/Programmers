# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/84512">모음사전</a>

### 문제설명

사전에 알파벳 모음 'A', 'E', 'I', 'O', 'U'만을 사용하여 만들 수 있는, 길이 5 이하의 모든 단어가 수록되어 있습니다. 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA"이며, 마지막 단어는 "UUUUU"입니다.

단어 하나 word가 매개변수로 주어질 때, 이 단어가 사전에서 몇 번째 단어인지 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - word의 길이는 1 이상 5 이하입니다.
 - word는 알파벳 대문자 'A', 'E', 'I', 'O', 'U'로만 이루어져 있습니다.

***

### 답안
``` csharp
using System;

public class Solution {
    public int solution(string word) {
        int answer = 0;
        // 계산용 더미 char 추가
        char[] answerWord = new char[5]{'Z','Z','Z','Z','Z'};
        string newWord = word;
        while(newWord.Length != 5) {
            newWord += "Z";
        }
        while(newWord != new string(answerWord)) {
            InitNextWord(answerWord, 0);
            answer++;
        }
        return answer;
    }
    void InitNextWord(char[] _word, int index){
        if(index == 4) {
            SetNextWord(_word, index);
        }else{
            switch(_word[index]) {
                case 'Z':
                    _word[index] = 'A';
                    break;
                default:
                    InitNextWord(_word, index + 1);
                    break;
            }
        }
    }
    void SetNextWord(char[] _word, int index) {
        switch(_word[index]) {
            case 'Z':
                _word[index] = 'A';
                break;
            case 'A':
                _word[index] = 'E';
                break;
            case 'E':
                _word[index] = 'I';
                break;
            case 'I':
                _word[index] = 'O';
                break;
            case 'O':
                _word[index] = 'U';
                break;
            case 'U':
                _word[index] = 'Z';
                if(index != 0) {
                SetNextWord(_word, index - 1);
                }
                break;
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (0.43ms, 30.9MB)
테스트 2 〉	통과 (0.50ms, 31MB)
테스트 3 〉	통과 (0.81ms, 31.5MB)
테스트 4 〉	통과 (0.84ms, 31.3MB)
테스트 5 〉	통과 (0.74ms, 31.2MB)
테스트 6 〉	통과 (0.56ms, 31MB)
테스트 7 〉	통과 (1.15ms, 31MB)
테스트 8 〉	통과 (0.61ms, 31.1MB)
테스트 9 〉	통과 (0.67ms, 30.8MB)
테스트 10 〉	통과 (0.58ms, 31.2MB)
테스트 11 〉	통과 (0.76ms, 31.1MB)
테스트 12 〉	통과 (0.54ms, 31.1MB)
테스트 13 〉	통과 (0.82ms, 31.2MB)
테스트 14 〉	통과 (0.69ms, 31MB)
테스트 15 〉	통과 (0.78ms, 31.3MB)
테스트 16 〉	통과 (0.73ms, 31.3MB)
테스트 17 〉	통과 (0.74ms, 31.2MB)
테스트 18 〉	통과 (0.59ms, 31.1MB)
테스트 19 〉	통과 (0.80ms, 31MB)
테스트 20 〉	통과 (0.56ms, 31MB)
테스트 21 〉	통과 (0.48ms, 31.2MB)
테스트 22 〉	통과 (0.55ms, 31.1MB)
테스트 23 〉	통과 (0.50ms, 31MB)
테스트 24 〉	통과 (0.56ms, 30.8MB)
테스트 25 〉	통과 (0.49ms, 31.2MB)
테스트 26 〉	통과 (0.55ms, 31.1MB)
테스트 27 〉	통과 (0.66ms, 30.9MB)
테스트 28 〉	통과 (0.80ms, 31.1MB)
테스트 29 〉	통과 (0.49ms, 30.8MB)
테스트 30 〉	통과 (0.51ms, 31MB)
테스트 31 〉	통과 (0.60ms, 31.1MB)
테스트 32 〉	통과 (0.69ms, 31.1MB)
테스트 33 〉	통과 (0.84ms, 31.1MB)
테스트 34 〉	통과 (0.72ms, 31MB)
테스트 35 〉	통과 (0.81ms, 31.3MB)
테스트 36 〉	통과 (0.79ms, 31MB)
테스트 37 〉	통과 (0.58ms, 30.9MB)
테스트 38 〉	통과 (0.63ms, 31.3MB)
테스트 39 〉	통과 (0.64ms, 31.2MB)
테스트 40 〉	통과 (0.59ms, 31.1MB)
```