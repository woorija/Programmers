# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42579">베스트앨범</a>

### 문제설명

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

 1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
 2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
 3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때, 베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

***

### 제한사항

 - genres[i]는 고유번호가 i인 노래의 장르입니다.
 - plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
 - genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
 - 장르 종류는 100개 미만입니다.
 - 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
 - 모든 장르는 재생된 횟수가 다릅니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Music : IComparable<Music> {
    public int index;
    public int play;
    public Music(int _index, int _play){
        index = _index;
        play = _play;
    }
    int IComparable<Music>.CompareTo(Music _other){
        int result = _other.play - play;
        if(result == 0){
            result = index - _other.index;
        }
        return result;
    }
}

public class Genre : IComparable<Genre> {
    public string name;
    public int play;
    public Genre(string _name, int _play){
        name = _name;
        play = _play;
    }
    int IComparable<Genre>.CompareTo(Genre _other){
        return _other.play - play;
    }
}

public class Solution {
    public int[] solution(string[] genres, int[] plays) {
        List<int> answer = new List<int>();
        Dictionary<string,List<Music>> dict = new Dictionary<string,List<Music>>();
        List<Genre> list = new List<Genre>();
        List<string> genreNames = new List<string>();
        for(int i = 0; i < genres.Length; i++) {
            if(!dict.ContainsKey(genres[i])) {
                dict.Add(genres[i], new List<Music>());
                list.Add(new Genre(genres[i], 0));
                genreNames.Add(genres[i]);
            }
            dict[genres[i]].Add(new Music(i, plays[i]));
            list[genreNames.IndexOf(genres[i])].play += plays[i];
        }
        
        list.Sort();
        foreach(var music in dict.Values) {
            music.Sort();
        }
        
        for(int i = 0; i < list.Count; i++) {
            string name = list[i].name;
            for(int j = 0; j < Math.Min(dict[name].Count, 2); j++) {
                answer.Add(dict[name][j].index);
            }
        }
        
        return answer.ToArray();
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (2.77ms, 31.3MB)
테스트 2 〉	통과 (2.76ms, 31.4MB)
테스트 3 〉	통과 (2.51ms, 31.1MB)
테스트 4 〉	통과 (1.91ms, 31.3MB)
테스트 5 〉	통과 (2.69ms, 31.3MB)
테스트 6 〉	통과 (2.70ms, 31.6MB)
테스트 7 〉	통과 (2.70ms, 31.4MB)
테스트 8 〉	통과 (2.73ms, 31.5MB)
테스트 9 〉	통과 (2.65ms, 31.2MB)
테스트 10 〉	통과 (2.79ms, 31.2MB)
테스트 11 〉	통과 (2.84ms, 31.5MB)
테스트 12 〉	통과 (2.73ms, 31.3MB)
테스트 13 〉	통과 (3.00ms, 31.7MB)
테스트 14 〉	통과 (2.71ms, 31.7MB)
테스트 15 〉	통과 (2.68ms, 31.3MB)
```