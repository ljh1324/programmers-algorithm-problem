# n진수 게임

## 코드
```cpp
#include <string>
#include <vector>

using namespace std;

const string numbers = "0123456789ABCDEF";

string decimalToBaseN(int decimal, int n) {
    string notation = "";
    do {
        notation = numbers[decimal % n] + notation;
        decimal /= n;
    } while (decimal != 0);
    
    return notation;
}

string solution(int n, int t, int m, int p) {
    string answer = "";
    string cur;
    int idx, order, cnt;
    int next = 0;
    
    order = cnt = 0;
    p--;
    while(cnt < t) {
        if (next == 0 || idx == cur.length()) {
            cur = decimalToBaseN(next, n);
            next++;
            idx = 0;
        }
        
        if (order % m == p) {
            answer += cur[idx];
            cnt++;
        }
        order++;
        idx++;
    }
    
    return answer;
}
```

## 풀이
- 10진수를 n진수로 변환하는 함수 정의
- 현재 숫자를 n진수로 변환한 문자열을 저장할 cur 변수 선언
- 다음 숫자를 나타내는 next 변수를 0으로 초기화
- 튜브가 말한 숫자 개수를 저장할 cnt 변수를 0으로 초기화
- 현재 순서를 나타내는 order 변수를 0으로 초기화
- 튜브의 순서 p를 1 감소 (0번째 부터 시작하도록 바꿈)
- cnt가 튜브가 말해야 하는 숫자 t 보다 작을 경우 반복문 수행
- next가 0이거나 지금 말해야할 idx번째 문자가 현재 문자열(cur)의 길이와 같을 경우 cur에 next를 n진법으로 변환한 문자열 저장 후 next 1 증가, idx를 0으로 초기화
- 만약 order % m이 p일 경우 answer에 현재 문자열의 idx번째 문자 추가, cnt 1 증가
- 다음 순서로 넘어가도록 order, idx 1 증가

## 다른 방법
- 말해야 하는 문자가 포함된 모든 숫자를 연결한 문자를 저장할 temp 선언
- 인원수에 튜브가 말해야하는 횟수를 곱하여 temp의 최대 길이를 mt에 저장
- num을 0에서 1씩 증가시키며 temp의 길이가 mt이하일 동안 반복하며 temp에 num을 n진수로 변환한 값을 연결해줌
- i를 0 ~ (t - 1) 동안 1씩 증가시키며 반복하며 answer에 temp의 `(m * i) + (p - 1)`번째 문자 추가