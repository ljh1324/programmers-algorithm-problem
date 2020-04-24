# 감시카메라

## 코드
```javascript
function solution(routes) {
    var answer = 0;
    var limit = -30001;
    
    routes.sort((a, b) => (a[1] - b[1]));
    
    routes.forEach(route => {
        if (limit < route[0]) {
            answer++;
            limit = route[1];
        } 
    });
    
    return answer;
}
```