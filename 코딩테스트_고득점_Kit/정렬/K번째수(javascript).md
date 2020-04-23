# K번째수

## 코드
```javascript
function solution(array, commands) {
    var answer = [];
    var cnt;
    var begin, end, k;
    
    array = array.map( (value, idx) => {
        return {value, idx: idx + 1};
    })
    
    array.sort((a, b) => {
        return a.value - b.value; 
    });
    
    commands.forEach(command => {
        [begin, end, k] = command;
        cnt = 0;
        array.forEach(element => {
            var {value, idx} = element;
            if (begin <= idx && idx <= end) {
                cnt++;
                if (cnt == k) answer.push(value);
            }
        });
    });
    
    return answer;
}
```