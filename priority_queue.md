# priority_queue

> **基本语法**

- 头文件是`#include<queue>`

- 模板申明：priority_queue<Type,Container,Functional>,其中Type为数据类型，Container为保存数据的容器，Functional为元素比较方式。

  Container必须是用数组实现的容器，比如vector，deque等等，但不能用list。STL里默认用的是vector。

> **自定义排序方法** 

- 重载operator<

  ```c++
  #include <iostream>
  #include <queue>
  using namespace std;
  struct Node
  {
      int x, y;
      Node(int a = 0, int b = 0) : x(a), y(b) {}
  };
  bool operator<(Node a, Node b) // 返回true时，说明a的优先级低于b,a放在后面
  {
      if (a.x == b.x)
          return a.y > b.y;
      return a.x > b.x;
  }
  int main()
  {
      priority_queue<Node> q;
      for (int i = 0; i < 10; ++i)
      {
          q.push(Node(rand(), rand()));
          while (!q.empty())
          {
              cout << q.top().x << ' ' << q.top().y << endl;
              q.pop();
          }
      }
      return 0;
  }
  ```

  

- 重写仿函数

  ```c++
  #include <iostream>
  #include <queue>
  using namespace std;
  struct Node
  {
      int x,y;
      Node(int a=0,int b=0):
          x(a),y(b){}
  };
  struct cmp
  {
      bool operator()(Node a,Node b)//默认是less函数
      {//返回true时，a的优先级低于b（a排在b的后面）
          if(a.x==b.x)
              return a.y>b.y;
          return a.x>b.x;
      }
  };
  int main()
  {
      priority_queue<Node,vector<Node>,cmp>q;
      for(int i=1;i<10;i++)
      {
          q.push(Node(rand(),rand()));
      }
      while(!q.empty())
      {
          cout<<q.top().x<<" "<<q.top().y<<endl;
          q.pop();
      }
      return 0;
  }
  ```

  