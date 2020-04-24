# 숫자 야구

## 코드
```javascript
function solution(baseball) {
    var answer = 0;
    var num, rs, rb, digit;
    var cs, cb;
    var a, b, c;    
    var flag;
    
    for (var i = 1; i <= 9; i++) {
        for (var j = 1; j <= 9; j++) {
            if (i == j) continue;
            
            for (var k = 1; k <= 9; k++) {
                if (i == k) continue;
                else if (j == k) continue;
                
                flag = baseball.reduce( (acc, game) => {
                    if (!acc) {
                        return acc;
                    }
                    
                    [num, rs, rb] = game;
                    c = num % 10;
                    b = parseInt(num / 10) % 10;
                    a = parseInt(num / 100);
                    
                    cs = cb = 0;
                    
                    if (i === a) cs++;
                    else if (j === a || k === a) cb++;
                    
                    if (j === b) cs++;
                    else if (i === b || k === b) cb++;
                    
                    if (k === c) cs++;
                    else if (j === c || i === c) cb++;
                    
                    if (cs !== rs || cb !== rb) {
                        acc = false;
                    }
                    return acc;
                }, true);
                
                if (flag) {
                    answer += 1;
                }
            }
        }
    }
    
    return answer;
}
```
