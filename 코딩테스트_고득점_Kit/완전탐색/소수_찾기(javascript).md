# 소수 찾기

## 코드
```javascript
var isPrime = [];
var cnt = 0;
var MAX = 10000000;

function checkPrime() {
  isPrime[0] = isPrime[1] = false;

  for (var i = 2; i < MAX; i += 1) {
    if (isPrime[i]) {
      for (var j = i + i; j < MAX; j += i) {
        isPrime[j] = false;
      }
    }
  }
}

function swap(arr, i, j) {
  var temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}

function countPrime(numbers, idx, length, acc) {
  if (idx === length) {
    if (acc === '') {
      return;
    }

    var num = parseInt(acc);
    if (isPrime[num]) {
      isPrime[num] = false;
      cnt++;
    }
    return;
  }

  for (var i = idx; i < length; i++) {
    swap(numbers, idx, i);
    countPrime(numbers, idx + 1, length, acc);
    countPrime(numbers, idx + 1, length, acc + numbers[idx]);
    swap(numbers, idx, i);
  }
}

function solution(numbers) {
  var answer = 0;
  var charArr = [];
    
  for (var i = 0; i < numbers.length; i++) {
      charArr.push(numbers.charAt(i));
  }
    
  for (var i = 0; i < MAX; i++) {
    isPrime.push(true);
  }
  checkPrime();

  countPrime(charArr, 0, numbers.length, '');
  answer = cnt;

  return answer;
}
```