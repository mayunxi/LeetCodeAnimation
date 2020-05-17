
#include <iostream>
#include <stack>
#include <vector>

using namespace std;

class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
            stack<int> stack1,stack2;
            vector<int> result(T.size(),0);
            for (int i= 0;i < T.size();i++)
            {
                if (!stack1.empty())
                {
                    while (T.at(i) > stack1.top())
                    {
                        result.at(stack2.top()) = i - stack2.top();
                        stack2.pop();
                        stack1.pop();
                        if (stack1.empty())
                        {
                            break;
                        }
                    }
                    stack1.push(T.at(i));
                    stack2.push(i);
                }
                else
                {
                    stack1.push(T.at(i));
                    stack2.push(i);
                }
            }
            return result;
    }

};

int main()
{

    vector<int> temp{73, 74, 75, 71, 69, 72, 76, 73};

    Solution s;
    vector<int> daily = s.dailyTemperatures(temp);

    return 0;

}

```
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
            stack<int> stack1,stack2;
            vector<int> result(T.size(),0);
            stack1.push(T.at(0));
            stack2.push(0);
            for (int i= 1;i < T.size();i++)
            {
                while (T.at(i) > stack1.top())
                {
                    result.at(stack2.top()) = i - stack2.top();
                    stack2.pop();
                    stack1.pop();
                    if (stack1.empty())
                    {
                        break;
                    }
                }
                stack1.push(T.at(i));
                stack2.push(i);
            }
            return result;
    }

};
```
