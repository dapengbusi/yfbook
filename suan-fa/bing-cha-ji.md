---
description: 并查集主要用于处理以下几个问题：
---

# 并查集

* 主要用于集合合并，快速查询某个元素跟另一个元素是否在同一个集合中。
* 可以在O(1)时间复杂度内，快速将两个元素合并到一起。
* 典型应用场景就是求图中的连通分量问题。

```
// 下面是一个并查集模版
// 优化策略有二：
// 1. 查询某个元素时，同时压缩路径，将元素往根上挂。
// 2. 合并两个不同的集合时，尽量将树高度小的往大的上面合并。

class UnionFind
{
private:
    vector<int> par;
    vector<int> rank;

public:
    UnionFind(int n) : par(n), rank(n, 0)
    {
        // 初始化每一个节点都是一个独立的元素
        for (int i = 0; i < n; i++)
        {
            par[i] = i;
        }
    }
    
    // 查询当前节点i到根节点
    // 这里做了一些优化，不是简单的，将集合叠加挂到根上，而是每次查询时，将当前节点的父亲节点设为根，让
    // 查询的元素尽量和根的距离为1，方便下次查找。
    // 所以保证了只要这个元素被访问过，则他的所有父亲都会把拍平
    int Find(int x)
    {
        // 只有查找的时候才会拍平树的高度
        if (par[x] != x)
        {
            par[x] = Find(par[x]);
        }
        return par[x];
    }
    
    // 合并两个元素
    // 1.先查找两个元素的根节点是否相同
    // 2.如果相同说明在同一个集合中，则直接返回。
    // 3.如果不相同，这里也有个优化，尽量把高度小的往大的上面放。
    bool UnionSet(int x, int y)
    {
        int xp = Find(x);
        int yp = Find(y);
        if (xp == yp)
        {
            return false;
        }

        if (rank[xp] < rank[yp])
        {
            par[xp] = yp;

            // 这里实际上对rank[xp]
            // 清零也可以，不过不用，因为后续他不是根，永远不会搜索到，除非有裂项的操作
            // rank[xp] = 0;
        }
        else if (rank[xp] > rank[yp])
        {
            par[yp] = xp;
        }
        else
        {
            // 这里并没有把路径拍平
            par[xp] = yp;
            rank[yp] += 1;
        }

        return true;
    }
};
```
