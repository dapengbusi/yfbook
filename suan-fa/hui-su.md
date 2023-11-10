# 回溯



````
// 经典回溯框架
```cpp
 void ParseDup(vector<int> &nums, vector<int> &tmp, int start)
    {
        ans.emplace_back(tmp);
        for (int i = start; i < nums.size(); i++)
        {
        
            // 这里针对去重的元素，如果没有去重可以不用
            if (i > start && nums[i] == nums[i - 1])
            {
                continue;
            }

            tmp.push_back(nums[i]);
            ParseDup(nums, tmp, i + 1);
            tmp.pop_back();
        }
    }
```
````
