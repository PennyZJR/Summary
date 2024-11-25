# Sort函数自定义cmp函数

> **只需记住当返回值为true时，第一个参数放在前面，第二个参数放在后面**

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;
//升序
bool cmp_up(int a, int b)
{
    if(a < b)
        return true;
    else
        return false;
}
//降序
bool cmp_down(int a, int b)
{
    if(a > b)
        return true;
    else
        return false;
}

int main()
{
    vector <int> array = {1,2,12,56,47,23,88,45,3,4,5,6,7};
    vector<int>::iterator it;

    cout << "asc order: ";
    sort(array.begin(), array.end(), cmp_up);//升序
    for (it = array.begin(); it != array.end(); it++) {
        cout << *it << " ";
    }
    cout << endl;

    cout << "desc order:";
    sort(array.begin(), array.end(), cmp_down);//降序
    for (it = array.begin(); it != array.end(); it++) {
        cout << *it << " ";
    }
    cout << endl;
    return 0;
}

```

