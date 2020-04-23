# H-Index

## 코드
```javascript
function solution(citations) {
    var answer = 0;
    var left, right, mid;
    var cnt = 0;
    
    left = 0; right = 1000;
    while (left <= right) {
        mid = parseInt((left + right) / 2);
        
        cnt = 0;
        citations.forEach(citation => {
            if (citation >= mid) {
                cnt++;
            }  
        });
        
        if (cnt >= mid) {
            left = mid + 1;
            answer = mid;
        } else {
            right = mid - 1;
        }
    }
    
    return answer;
}
```

## 풀이
- 이진탐색 알고리즘 사용