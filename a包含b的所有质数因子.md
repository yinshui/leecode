#### 题目描述
判断a是不是包含b的所有质数因子。  

#### 思路
类似竖除求出b的所有质数因子，顺便逐个判断a有没有这个因子。  

但是会超时，于是剪枝。  
```cpp
#include<iostream>
using namespace std;
int main()
{
    long long int a= 9299995937, b= 9955999937;
    cout << a << b << endl;
    //cin >> a >> b;
    long long int i = 2;
    bool flag = false;
    while (i <= sqrt(b)||i<=sqrt(a))//只需要循环到这里就好了
    {
        if (a%b == 0) {//剪枝
            break;
        }
        long long int j = b % i;
        if (j == 0)
        {
            b = b / i;
            if (a%i != 0)
            {
                flag = true;
                break;
            }
        }
        else {
            i++;
        }
    }
    cout << i << endl;
    if (a%b != 0) {
        cout << "No";
    }
    else if (flag)
        cout << "No";
    else cout << "Yes";
    cout << endl;
    return 0;
}
```