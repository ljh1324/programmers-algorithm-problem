# 가장 큰 수

## 코드
```javascript
function solution(numbers) {
    var answer = '';
    
    numbers = numbers.map(number => number.toString());
    
    numbers.sort((a, b) => {
        var r1 = a + b;
        var r2 = b + a;
        
        if (r1 === r2) return 0;
        else if (r1 > r2) return -1;
        else return 1;
    });
    
    answer = numbers.reduce((acc, number) => {
        return acc + number;
    }, '');
    
    if (parseInt(answer) === 0) {
        return '0';
    }
    
    return answer;
}
```