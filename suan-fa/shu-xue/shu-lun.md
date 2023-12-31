# 数论

## #参考文档

* [https://www.cnblogs.com/vongang/archive/2013/03/10/2952978.html](https://www.cnblogs.com/vongang/archive/2013/03/10/2952978.html)

## 同余定理

* 如果 (a-b) 能被m整除，那么a和b对m同余。

举个例子，如15-3 = 12 能被2 整除，那么15 和 3 对2取模相等，都等于1。可以理解为两数之差能被表达成两个数乘积，那么这前者，对后者任意一个数取余都相同。

leetcode求 连续子数组和是否是k的倍数，可以用前缀和判断一个区间，对k是否同余，这个是典型的同余的应用。

## 模运算

&#x20;模运算与基本[四则运算](https://baike.baidu.com/item/%E5%9B%9B%E5%88%99%E8%BF%90%E7%AE%97/5337481?fromModule=lemma\_inlink)有些相似，但是除法例外。其规则如下：

1. (a + b) % p = (a % p + b % p) % p （1）
2. (a - b) % p = (a % p - b % p ) % p （2）
3. (a \* b) % p = (a % p \* b % p) % p （3）
4. a ^ b % p = ((a % p)^b) % p （4）

### 加法模运算应用

如前缀和取模时，可以对每一项取模，再加和

```
//求前缀和模k的算法
int r = 0;
for(int i = 0; i < m; i++){
    r = (r+nums[i]) % k
    // 这部分等价于 (r + nums[i]%k) %k 由于 num[i]%k 和 num[i]对k同余，所以结果不会发生改变。
}
```

### 乘法和加法线性同余公式应用

* (a+b+c+d)%m = (a%m + b%m + c%m + d%m) %m
* (a\*b\*c)%m = (a%m \* b%m \* c%m) %m



```
// 求 1 11 111 1111 11111 是否是k的倍数
1.本质是求 （num * 10+1）% k 的问题， num会比较大，我们看看num跟 num%k = r的关系
2.(num * 10 +1) % k = (（num%k * 10 %k）%k + 1%k) %k = ((r * 10%k)%k+ 1%k)%k = (r * 10%k +1)%k)

int n = 1;
while(n%k !=0){
n = (n*10 + 1)%k;
}


```



\
