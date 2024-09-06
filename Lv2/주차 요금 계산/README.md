# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/92341">주차 요금 계산</a>

### 문제설명

주차장의 요금표와 차량이 들어오고(입차) 나간(출차) 기록이 주어졌을 때, 차량별로 주차 요금을 계산하려고 합니다. 아래는 하나의 예시를 나타냅니다.

 - 요금표
| 기본 시간(분) | 기본 요금(원) | 단위 시간(분) | 단위 요금(원) |
| ------- | ------- | ------- | ------- |
| 180 | 5000 | 10 | 600 |

 - 입/출차 기록
| 시각(시:분) | 차량 번호 | 내역 |
| ------- | ------- | ------- |
| 05:34 | 5961 | 입차 |
| 06:00 | 0000 | 입차 |
| 06:34 | 0000 | 출차 |
| 07:59 | 5961 | 출차 |
| 07:59 | 0148 | 입차 |
| 18:59 | 0000 | 입차 |
| 19:09 | 0148 | 출차 |
| 22:59 | 5961 | 입차 |
| 23:00 | 5961 | 출차 |

 - 자동차별 주차 요금
| 차량 번호 | 누적 주차 시간(분) | 주차 요금(원) |
| ------- | ------- | ------- |
| 0000 | 34 + 300 = 334 | 5000 + ⌈ (334 - 180) / 10 ⌉ x 600 = 14600 |
| 0148 | 670 | 5000 + ⌈ (670 - 180) / 10 ⌉ x 600 = 34400 |
| 5961 | 145 + 1 = 146 | 5000 |

 - 어떤 차량이 입차된 후에 출차된 내역이 없다면, 23:59에 출차된 것으로 간주합니다.
   - 0000번 차량은 18:59에 입차된 이후, 출차된 내역이 없습니다. 따라서, 23:59에 출차된 것으로 간주합니다.
 - 00:00부터 23:59까지의 입/출차 내역을 바탕으로 차량별 누적 주차 시간을 계산하여 요금을 일괄로 정산합니다.
 - 누적 주차 시간이 기본 시간이하라면, 기본 요금을 청구합니다.
 - 누적 주차 시간이 기본 시간을 초과하면, 기본 요금에 더해서, 초과한 시간에 대해서 단위 시간 마다 단위 요금을 청구합니다.
   - 초과한 시간이 단위 시간으로 나누어 떨어지지 않으면, 올림합니다.
   - ⌈a⌉ : a보다 작지 않은 최소의 정수를 의미합니다. 즉, 올림을 의미합니다.

주차 요금을 나타내는 정수 배열 fees, 자동차의 입/출차 내역을 나타내는 문자열 배열 records가 매개변수로 주어집니다. 차량 번호가 작은 자동차부터 청구할 주차 요금을 차례대로 정수 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

***

### 제한사항

 - fees의 길이 = 4
   - fees[0] = 기본 시간(분)
   - 1 ≤ fees[0] ≤ 1,439
   - fees[1] = 기본 요금(원)
   - 0 ≤ fees[1] ≤ 100,000
   - fees[2] = 단위 시간(분)
   - 1 ≤ fees[2] ≤ 1,439
   - fees[3] = 단위 요금(원)
   - 1 ≤ fees[3] ≤ 10,000

 - 1 ≤ records의 길이 ≤ 1,000
   - records의 각 원소는 "시각 차량번호 내역" 형식의 문자열입니다.
   - 시각, 차량번호, 내역은 하나의 공백으로 구분되어 있습니다.
   - 시각은 차량이 입차되거나 출차된 시각을 나타내며, HH:MM 형식의 길이 5인 문자열입니다.
     - HH:MM은 00:00부터 23:59까지 주어집니다.
     - 잘못된 시각("25:22", "09:65" 등)은 입력으로 주어지지 않습니다.
   - 차량번호는 자동차를 구분하기 위한, `0'~'9'로 구성된 길이 4인 문자열입니다.
   - 내역은 길이 2 또는 3인 문자열로, IN 또는 OUT입니다. IN은 입차를, OUT은 출차를 의미합니다.
   - records의 원소들은 시각을 기준으로 오름차순으로 정렬되어 주어집니다.
   - records는 하루 동안의 입/출차된 기록만 담고 있으며, 입차된 차량이 다음날 출차되는 경우는 입력으로 주어지지 않습니다.
   - 같은 시각에, 같은 차량번호의 내역이 2번 이상 나타내지 않습니다.
   - 마지막 시각(23:59)에 입차되는 경우는 입력으로 주어지지 않습니다.
   - 아래의 예를 포함하여, 잘못된 입력은 주어지지 않습니다.
     - 주차장에 없는 차량이 출차되는 경우
     - 주차장에 이미 있는 차량(차량번호가 같은 차량)이 다시 입차되는 경우

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class Solution {
    Dictionary<int,int> timeTable;
    SortedDictionary<int,int> sheet;
    public int[] solution(int[] fees, string[] records) {
        timeTable = new Dictionary<int,int>();
        sheet = new SortedDictionary<int,int>();
        List<int> answer;
        
        for(int i = 0; i < records.Length;i++){
            string[] infor = records[i].Split(" ");
            string[] times = infor[0].Split(":");
            int time = int.Parse(times[0]) * 60 + int.Parse(times[1]);
            int num = int.Parse(infor[1]);
            
            if(infor[2] == "IN"){
                timeTable.Add(num, time);
            }else{
                Out(num, time);
                timeTable.Remove(num);
            }
        }
        foreach(var infor in timeTable){
            int time = 1439;
            int num = infor.Key;
            Out(num, time);
        }
        answer = new List<int>(sheet.Values);
        for(int i = 0; i < answer.Count; i++) {
            int time = answer[i];
            if(time <= fees[0]) {
                answer[i] = fees[1];
            }else{
                time = (int)Math.Ceiling((double)(time - fees[0]) / fees[2]);
                answer[i]=fees[1] + time * fees[3];
            }
        }
        return answer.ToArray();
    }
    void Out(int _num, int _time) {
        int addTime = _time - timeTable[_num];
        if(sheet.ContainsKey(_num)) {
            sheet[_num] += addTime;
        }else{
            sheet.Add(_num, addTime);
        }
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (8.54ms, 31.8MB)
테스트 2 〉	통과 (7.85ms, 31.8MB)
테스트 3 〉	통과 (9.16ms, 31.6MB)
테스트 4 〉	통과 (8.45ms, 31.8MB)
테스트 5 〉	통과 (7.29ms, 32MB)
테스트 6 〉	통과 (8.10ms, 32MB)
테스트 7 〉	통과 (9.34ms, 32MB)
테스트 8 〉	통과 (11.28ms, 32.4MB)
테스트 9 〉	통과 (7.78ms, 31.7MB)
테스트 10 〉	통과 (14.00ms, 32.3MB)
테스트 11 〉	통과 (9.04ms, 32.4MB)
테스트 12 〉	통과 (10.73ms, 32.3MB)
테스트 13 〉	통과 (7.66ms, 31.6MB)
테스트 14 〉	통과 (7.22ms, 31.6MB)
테스트 15 〉	통과 (5.97ms, 31.6MB)
테스트 16 〉	통과 (5.95ms, 31.9MB)
```