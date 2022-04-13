# Backtrack 回溯

# 模板

- 回溯是递归的副产品，有递归就可以有回溯

- 回溯的效率其实很低，本质是穷举所有可能然后选出想要的答案

- 可以解决的问题：

  - 组合问题： N个数里面按一定规则找出k个数的集合
  - 排列问题：N个数按照一定规则全排列，有几种排列方式
  - 切割问题：一个字符串按一定规则有几种切割方式
  - 子集问题： 一个N个数的集合有多少符合条件的子集
  - 棋盘问题：N皇后，解数独

- 理解回溯： **抽象为树形结构**

  - 集合大小构成了树的宽度，递归的深度构成树的深度
  - 递归有终止条件所以一定深度有限

- 代码模板

  ```
  void backtracking(参数) {
      if (终止条件) {
          存放结果;
          return;
      }
  
      for (选择：本层集合中元素（树中节点孩子的数量就是集合的大小）) {
          处理节点;
          backtracking(路径，选择列表); // 递归
          回溯，撤销处理结果
      }
  }
  
  ```

![回溯算法理论基础](https://camo.githubusercontent.com/f65ca647f31913496481cd1aff144040bd7ee4f6bc30accd370bc78b4b265d13/68747470733a2f2f696d672d626c6f672e6373646e696d672e636e2f32303231303133303137333633313137342e706e67)

从图中看出**for循环可以理解是横向遍历，backtracking（递归）就是纵向遍历**，这样就把这棵树全遍历完了，一般来说，搜索叶子节点就是找的其中一个结果了。

### 1. 17 数字键盘组合Letter Combinations of a Phone Number (Medium)

[Leetcode](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/) / [力扣](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/description/)

题目描述：Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

时间复杂度：O（n*4^n）

空间复杂度：

```c++
class Solution {
public:
    string path;
    vector<string> result;
    const vector<string> pad={"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    vector<string> letterCombinations(string digits) {
        if(digits.length()==0)
            return result;
        backtrack(0,digits);
        return result;
    }
    void backtrack(int index,string digits)
    {
        if(path.length()==digits.length())
        {
            result.push_back(path);
            return;
        }
        else
        {
            string s = pad[digits[path.length()]-'0'];
            for (int i=0;i<s.length();i++)
            {
                path.push_back(s[i]);
                backtrack(index+1,digits);
                path.pop_back();
            }
        }
    }
};
```

