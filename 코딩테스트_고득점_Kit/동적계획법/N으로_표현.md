# N으로 표현

## 코드
```cpp
#include <string>
#include <vector>

using namespace std;

int answer = 9;

// num가 target이 될 때까지 N을 이어붙여 사칙 연산을 하는 깊이 우선 탐색 함수
void dfs(int target, int num, int count, int N) {
    // num가 target이고 count가 answer보다 작을 경우 answer에 count 저장
    if (target == num) {
        if (count < answer) {
            answer = count;
        }
        return;
    }

    // count가 8이상일 경우 더 이상 탐색할 필요가 없으므로 return    
    if (count >= 8) return;
    
    int acc = 0;
    for (int i = 1; i <= 8 - count; i++) {
        acc = acc * 10 + N; // 반복문을 수행하면서 N을 i번 만큼 사용

        // num에 '+', '-', '*', '/' 연산을 수행
        dfs(target, num + acc, count + i, N);
        dfs(target, num - acc, count + i, N);
        dfs(target, num * acc, count + i, N);
        dfs(target, num / acc, count + i, N);
    }
}

int solution(int N, int number) {
    dfs(number, 0, 0, N);
    
    if (answer >= 9) answer = -1;
    
    return answer;
}
```

## 풀이
- N을 최대 8번까지 사용할 수 있으므로 answer에 9를 저장
- 반복문을 수행하면서 N을 i번 만큼 사용한 숫자를 acc변수에 저장. 기존 계산된 숫자에 acc값을 사칙연산을 하는 재귀함수를 통해 최솟값을 찾아냄

## 다른 방법
- count가 최솟값보다 클 경우 return을 하여 속도를 개선할 수 있음
- N을 n번 사용하여 만들 수 있는 숫자를 구할 때 1 ~ (n - 1) 만큼 반복문을 수행하면서 N을 i번 사용하여 만들 수 있는 숫자와 N을 (n - i)번 사용하여 만들 수 있는 숫자를 구하고 두 집합의 원소를 꺼내어 사칙연산하여 n번 사용하여 만들 수 있는 숫자에 추가하는 재귀적 함수 정의

```cpp
unordered_set<int> cache[10];

unordered_set<int> solve(int n) {
    if (!cache[n].empty()) return cache[n]; // 캐싱된 값 반환

    int num = 0;
    for (int i = 0; i < n; i++) num = 10 * num + N;
    unordered_set<int> res;
    res.insert(num); // N을 n번 사용하는 경우의 수를 추가
    for (int i = 1; i < n; i++) {
        int j = n - i;
        auto s1 = solve(i);
        auto s2 = solve(j);
        for (int n1 : s1) {
            for (int n2 : s2) {
                res.insert(n1 + n2);
                res.insert(n1 - n2);
                res.insert(n1 * n2);
                if (n2 != 0) res.insert(n1 / n2);
            }
        }
    }
    return cache[n] = res;
}
```