# H-Index

## 코드
```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    int answer = 0;
    
    sort(citations.begin(), citations.end());
    
    for (int i = citations.size() - 1; i >= 0; i--) {
        answer++;
        if (citations[i] < answer) {
            answer--;
            break;
        }
    }   
    
    return answer;
}
```

## 풀이
- 논문별 인용 횟수를 오름차순 정렬
- 끝에서 부터 H-Index(answer)를 증가시키면서 H-Index 이상 인용했는지 확인하는 반복문 수행
- H-Index 보다 적게 인용되었을 경우 H-Index를 감소시킨 후 반복문 종료 

## 다른 방법
- 적절한 H-Index를 찾는 이진탐색 알고리즘 사용