# <a href="https://school.programmers.co.kr/learn/courses/30/lessons/42627">디스크 컨트롤러</a>

### 문제설명

하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다.

가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어

```
 - 0ms 시점에 3ms가 소요되는 A작업 요청
 - 1ms 시점에 9ms가 소요되는 B작업 요청
 - 2ms 시점에 6ms가 소요되는 C작업 요청
```
와 같은 요청이 들어왔습니다.

한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.

```
 - A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
 - B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
 - C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
```

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면

```
 - A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
 - C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
 - B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
```

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

***

### 제한사항

 - jobs의 길이는 1 이상 500 이하입니다.
 - jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
 - 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
 - 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
 - 하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

***

### 답안
``` csharp
using System;
using System.Collections.Generic;

public class JobData:IComparable<JobData> {
    public int start;
    public int time;
    public int sortType;
    public JobData(int _start, int _time) {
        start = _start;
        time = _time;
        sortType = 0;
    }
    public void ChangeSortType() {
        sortType = 1;
    }
    int IComparable<JobData>.CompareTo(JobData _other) {
        if(sortType == 0) {
            if (start != _other.start)
            {
                return start.CompareTo(_other.start);
            }
            return _other.time.CompareTo(time);
        }else{
            return time.CompareTo(_other.time);
        }
    }
}

public class Solution {
    public int solution(int[,] jobs) {
        int answer = 0;
        int currentTime = 0;
        int total = jobs.GetLength(0);
        List<int> times = new List<int>();
        List<JobData> datas = new List<JobData>();
        
        for(int i = 0; i < jobs.GetLength(0); i++) {
            datas.Add(new JobData(jobs[i,0], jobs[i,1]));
        }
        
        datas.Sort();
        for(int i = 0; i < datas.Count; i++) {
            datas[i].ChangeSortType();
        }
        
        List<JobData> queue = new List<JobData>();
        
        while(times.Count != total) {
            int count = 0;
            for(int i = 0; i < datas.Count; i++) {
                if(datas[i].start > currentTime) {
                    break;
                } 
                queue.Add(datas[i]);
                count++;
            }
            if(queue.Count == 0) {
                currentTime = datas[0].start;
                continue;
            }
            datas.RemoveRange(0, count);
            queue.Sort();
            
            JobData currentData = queue[0];
            currentTime += currentData.time;
            times.Add(currentTime - currentData.start);
            queue.RemoveAt(0);
        }
        
        int sum = 0;

        for(int i = 0; i < times.Count; i++) {
            sum += times[i];
        }
        answer = sum / times.Count;
        return answer;
    }
}
```

***

### 정확성 테스트
```
테스트 1 〉	통과 (9.44ms, 31.2MB)
테스트 2 〉	통과 (8.05ms, 31.2MB)
테스트 3 〉	통과 (6.40ms, 31.4MB)
테스트 4 〉	통과 (6.29ms, 31.4MB)
테스트 5 〉	통과 (8.84ms, 31.2MB)
테스트 6 〉	통과 (2.16ms, 31.3MB)
테스트 7 〉	통과 (5.83ms, 31.3MB)
테스트 8 〉	통과 (4.33ms, 31.5MB)
테스트 9 〉	통과 (2.52ms, 31.5MB)
테스트 10 〉	통과 (10.44ms, 31MB)
테스트 11 〉	통과 (1.98ms, 31.3MB)
테스트 12 〉	통과 (2.09ms, 31.4MB)
테스트 13 〉	통과 (2.01ms, 30.8MB)
테스트 14 〉	통과 (2.00ms, 31.2MB)
테스트 15 〉	통과 (1.96ms, 30.9MB)
테스트 16 〉	통과 (1.94ms, 31MB)
테스트 17 〉	통과 (3.01ms, 31.4MB)
테스트 18 〉	통과 (2.09ms, 31.4MB)
테스트 19 〉	통과 (2.06ms, 31.2MB)
테스트 20 〉	통과 (1.37ms, 31.2MB)
```