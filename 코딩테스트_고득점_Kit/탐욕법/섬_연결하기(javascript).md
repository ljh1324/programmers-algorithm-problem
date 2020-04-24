# 섬 연결하기

## 코드
```javascript
class DisjointSet {
    constructor(n) {
        this.parent = [];
        this.rank = [];
        
        for (var i = 0; i < n; i++) {
            this.parent.push(i);
            this.rank.push(1);
        }
    }
    
    find(u) {
        if (this.parent[u] === u) return u;
        return this.parent[u] = this.find(this.parent[u]);
    }
    
    merge(u, v) {
        u = this.find(u);
        v = this.find(v);
        
        if (this.rank[u] > this.rank[v]) {
            var temp = u;
            u = v;
            v = temp;
        }
        
        this.parent[u] = v;
        if (this.rank[u] === this.rank[v]) this.rank[v]++;
    }
}

function solution(n, costs) {
    var answer = 0;
    var u, v, c;
    var pu, pv;
    var set = new DisjointSet(n);
    
    costs.sort((a, b) => a[2] - b[2]);
    
    costs.forEach(cost => {
        [u, v, c] = cost;
        
        if (set.find(u) !== set.find(v)) {
            set.merge(u, v);
            answer += c;
        }
    });
    
    return answer;
}
```