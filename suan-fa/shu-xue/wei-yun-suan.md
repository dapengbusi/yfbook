# 位运算

## 位运算实现加法

主要基于两点

* 两个数字的异或运算是不进位的加法 得到新的a
* a\&b 然后，右移一位得到新的b
* 继续循环上述操作，直到b为0

```cpp
int getSum(int a, int b) {

        while(b){
            int t = a ^b;
            b =  (a & b) << 1;
            a = t;
        }
        return a;
}
```

```
```
