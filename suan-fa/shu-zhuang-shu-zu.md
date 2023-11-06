---
description: 树状数组模版 主要处理前N项和中元素有变动时，如何快速获得区间前n项和。
---

# 树状数组

## 树状数组模版 主要处理前N项和中元素有变动时，如何快速获得区间前n项和。

### 1.针对的问题：

* 单点修改
* 区间内查询前n项和，n项乘
* 说白了就是前n项和的快速处理

### 2.核心原理

* 每个位置x都划分一个管辖范围，管辖范围为lowbit(x)大小
* 每个位置x的父亲为x+lowbit(x)
* &#x20;修改某个位置的值，只修改子和所有父亲的节点
* &#x20;求某个区间\[l,r]的和

### 3.注意事项：

* tree的下标一定从1开始
* &#x20;区间下标的求和下标对应的是原数组下标



````
```cpp
class treeArray{
    private:
    // 原数组
    vector<int> nums_;
    // 区间和数组
    vector<int> tree_;

        //下标x的管辖范围
    int lowbit(int x){
        return x&-x;
    }

    // 构建树，把u加到对应节点上
    void add(int x, int u){
        while(x <  tree_.size()){
            tree_[x] += u;
            x += lowbit(x);
        }
    }

    // 查询前x项和
    int query(int x){
        int ans = 0;
        while(x){
            ans += tree_[x];
            x -= lowbit(x);
        }
        return ans;
    }

    public:
    treeArray(vector<int> nums):nums_(nums),tree_(nums.size()+1){
        // 初始化每个区间和，就是把nums[i]加到对应的父节点链路上
        for(int i = 0; i < nums.size(); i++){
            add(i+1,nums[i]);
        }
    }
    
    // 修改单点的值 下标也是原数组下标
    void update(int x, int u){
        add(x+1,u-nums_[x]);
        nums_[x] = u;
    }

    // 查询区间和，注意下标是原数组下标
    int getRangeSum(int l , int r){
        return query(r+1) - query(l);
    }
};
```
````

```markdown
```
