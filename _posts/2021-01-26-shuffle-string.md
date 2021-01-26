---
title: shuffle string
layout: post
categories: c++
date:   2021-01-26 12:30:08 +0800
tags: c++
excerpt: sort string by vector
---
--------------------
文章出自个人博客，转载请申明

------------------
# 目录 <span id="home">
* [问题](#1)
* [分析](#2)
* [解决方案](#3)
	* [方法一](#3.1)
	
----------------------------
# 问题 <span id="1">

[shuffle-string](https://leetcode-cn.com/problems/shuffle-string	"https://leetcode-cn.com/problems/shuffle-string")
给你一个字符串 s 和一个 长度相同 的整数数组 indices 。
请你重新排列字符串 s ，其中第 i 个字符需要移动到 indices[i] 指示的位置。
返回重新排列后的字符串。

**示例 1：**
```
输入：s = "codeleet", indices = {4,5,6,7,0,2,1,3}
输出："leetcode"
解释：如图所示，"codeleet" 重新排列后变为 "leetcode" 。
```

**示例 2：**

```
输入：s = "abc", indices = {0,1,2}
输出："abc"
解释：重新排列后，每个字符都还留在原来的位置上。
```

**示例 3：**

```
输入：s = "aiohn", indices = {4,1,3,0,2}
输出："nihao"
```

**示例 4：**

```
输入：s = "aaiougrt", indices = {4,0,2,6,7,3,1,5}
输出："uairtoag"
```

**示例 5：**

```
输入：s = "art", indices = {1,0,2}
输出："rat"
```


# 分析 <span id="2">

You can create an auxiliary string t of length n.

Assign t[indexes[i]] to s[i] for each i from 0 to n-1.

# 解决方案 <span id="3">

## 方法一 <span id="3.1">

```c
class Solution
{
private:
    /* data */
public:
    Solution(/* args */);
    ~Solution();
    static void restoreString(string& s, vector<int>& indices);
    static void test()
    {
        test0();
        test1();
        test2();
        test3();
        test4();
    }

    static void test0()
    {
        string s1 = "codeleet";
        int arr1[] = {4,5,6,7,0,2,1,3};
        vector<int> iv1(begin(arr1), end(arr1));
        restoreString(s1, iv1);
    }

    static void test1()
    {
        string s = "aiohn";
        int arr[] = { 4,1,3,0,2};
        vector<int> iv(begin(arr), end(arr));
        restoreString(s, iv);
    }

    static void test2()
    {
        string s = "abc";
        int arr[] = {0,1,2};
        vector<int> iv(begin(arr), end(arr));
        restoreString(s, iv);
    }

    static void test3()
    {
        string s = "aaiougrt";
        int arr[] = {4,0,2,6,7,3,1,5};
        vector<int> iv(begin(arr), end(arr));
        restoreString(s, iv);
    }

    static void test4()
    {
        string s = "art";
        int arr[] = {1,0,2};
        vector<int> iv(begin(arr), end(arr));
        restoreString(s, iv);
    }
};

Solution::Solution(/* args */)
{
}

Solution::~Solution()
{
}

void Solution::restoreString(string& s, vector<int>& indices)
{
    cout<<s<<endl;
    for (auto c : indices)
        cout << c << ' ';
    cout << endl;

    if(s.length() != indices.size())
    {
        printf("error: s: %lu != %lu vector\n", s.length(), indices.size());
        return;
    }

    string t = s;

    for(size_t i = 0; i < s.length(); i++)
    {
        s[i] = t[indices[i]];
    }

    cout << s << endl << endl;
}

int main(int argc, char *argv[])
{
    Solution::test();
    return 0;
}
```