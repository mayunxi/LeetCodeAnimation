### 数组的优缺点
要掌握一种数据结构，就必须要懂得分析它的优缺点。数组优点在于：
* 构建非常简单
* 能在O(1)的时间里根据数组下标(index)查询某个元素

而数组的缺点在于：
* 构建时必须分配一段连续空间
* 查询某个元素是否存在时需要遍历整个数组，耗费O(n)的时间（其中n是元素个数）
* 删除和添加某个元素，同样需要耗费O(n)时间

所以，当你在考虑是否应当采用数组去辅助你的算法时，请务必考虑它的优缺点，看看它的缺点是否会阻碍你的算法复杂度以及空间复杂度。

##### 242. 有效的字母异位词
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例 1:

输入: s = "anagram", t = "nagaram"

输出: true

示例 2:

输入: 
s = "rat", t = "car"

输出:
false

说明:你可以假设字符串只包含小写字母。

第一次提交：
```
class Solution {
public:
    bool isAnagram(string s, string t) {

        char  small_letter[26]={0};
        if (s.length()!= t.length())
        {
            return false;
        }
        else
        {
            int i;
            for (i = 0;i < s.length();i++)
            {
                small_letter[s[i]-97]++;
            }
            for (i = 0;i < t.length();i++)
            {
                small_letter[t[i]-97]--;
            }
            bool sum = true;
            for (i= 0;i<26;i++)
            {
                if (small_letter[i] !=0)
                {
                    sum = false;
                    break;
                }
            }
            if (sum)
            {
                printf("true\n");
                return true;
            }
            else
            {
                printf("false\n");
                return false;
            }
        }
    }
};
```
第二次提交：
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length()!= t.length())
            return false;
        char  small_letter[26]={0};
        for (auto ch:s)
        {
            small_letter[ch-'a']++;
        }
        for (auto ch:t)
        {
            small_letter[ch-'a']--;
        }
        for (auto i:small_letter)
        {
            if (i !=0)
            {
                return false;
            }
        }
        return true;
        }
};
```
第三次提交：
```
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length()!= t.length())
            return false;
        char  small_letter[26]={0};
        for (int i = 0;i < s.length();i++)
        {
            ++small_letter[s[i]-'a'];
            --small_letter[t[i]-'a'];
        }
        for (auto i:small_letter)
        {
            if (i !=0)
            {
                return false;
            }
        }
        return true;
        }
};
```
