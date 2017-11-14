# Implement pow(x, n).

# 解题思路
pow(x,n)就是x^n,,可以看成是x乘以n次。。。为了提高效率，可以将直接写x*=x;然后n相应除以2。。。
因此当n为单数时，则x*pow(x*x,n/2)

# 代码实现

``` javascript
var myPow = function(x, n) {    
    if(n==0)
        return 1;
    if(n<0){
        n = -n;
        x = 1/x;
    }
    return (n%2===0) ? myPow(x*x,Math.floor(n/2)) : x*myPow(x*x,Math.floor(n/2));
};
```