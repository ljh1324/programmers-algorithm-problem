# K번째수

## 코드
```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <utility>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;
    vector<pair<int, int>> arrayWithIndex;
    int arraySize = array.size();
    int commandsSize = commands.size();
    int i, j, cnt, begin, end, k, idx;
    
    // index 정보와 함께 배열 원소 저장
    for (i = 0; i < arraySize; i++) {
        arrayWithIndex.push_back(make_pair(array[i], i + 1));
    }
    
    // 전체 배열 sort
    sort(arrayWithIndex.begin(), arrayWithIndex.end());
    
    for (i = 0; i < commandsSize; i++) {
        begin = commands[i][0];
        end = commands[i][1];
        k = commands[i][2];
        cnt = 0;
        for (j = 0; j < arraySize; j++) {
            idx = arrayWithIndex[j].second;
            // index가 begin번째 end번째 사이일 경우 cnt 증가
            if (begin <= idx && idx <= end) {
                cnt++;
                // cnt가 k번째 숫자일 경우 break
                if (cnt == k) break;
            }
        }
        // k번째 숫자를 answer에 추가
        answer.push_back(arrayWithIndex[j].first);
    }
    
    return answer;
}
```

## 풀이
- 각 원소에 index 정보도 함께 저장하여 정렬
- 정렬된 배열 원소의 index가 command의 begin번째 end번째 사이에 있을 경우 cnt를 증가시킴
- cnt가 k일 경우 break를 하여 k번째 숫자를 answer에 추가

## 다른 방법
- 메모리가 충분하다면 begin, end, k를 찾을 때 마다 캐싱하여 속도를 더 높일 수 있을 것 같음
- segment tree를 사용하는 방법도 존재