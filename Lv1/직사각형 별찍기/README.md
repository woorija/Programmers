# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/12969">직사각형 별찍기</a>

### 문제설명

이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.

별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.

***

### 제한사항

 - n과 m은 각각 1000 이하인 자연수입니다.

***

### 답안
``` csharp
using System;

public class Example
{
    public static void Main()
    {
        String[] s;

        Console.Clear();
        s = Console.ReadLine().Split(' ');

        int a = Int32.Parse(s[0]);
        int b = Int32.Parse(s[1]);
        
        string str = "";
        for(int i = 0; i < a; i++) {
            str += "*";
        }
        for(int i = 0; i < b; i++) {
            Console.WriteLine(str);
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (16.92ms, 16.5MB)
테스트 2 〉	통과 (17.06ms, 16.6MB)
테스트 3 〉	통과 (17.39ms, 16.8MB)
테스트 4 〉	통과 (19.64ms, 16.6MB)
테스트 5 〉	통과 (18.69ms, 16.6MB)
테스트 6 〉	통과 (18.17ms, 16.8MB)
테스트 7 〉	통과 (17.55ms, 16.5MB)
테스트 8 〉	통과 (19.38ms, 17.7MB)
테스트 9 〉	통과 (17.65ms, 16.7MB)
테스트 10 〉	통과 (19.57ms, 17.3MB)
테스트 11 〉	통과 (17.91ms, 16.5MB)
```