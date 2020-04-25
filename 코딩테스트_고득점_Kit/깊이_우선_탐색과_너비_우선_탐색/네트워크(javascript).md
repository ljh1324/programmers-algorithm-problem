# 네트워크

## 코드
```javascript
var visited = [];

function dfs(n, computers, u) {
    for (var i = 0; i < n; i++) {
        if (i === u || visited[i] || !computers[u][i]) {
            continue;
        }
        
        visited[i] = true;
        dfs(n, computers, i);
    }
}

function solution(n, computers) {
    var answer = 0;
    
    for (var i = 0; i < n; i++) {
        visited.push(false);
    }
    
    for (var i = 0; i < n; i++) {
        if (!visited[i]) {
            visited[i] = true;
            answer += 1;
            dfs(n, computers, i);
        }
    }
    
    return answer;
}
```