# ACM模式构建二叉树

```c++
#include <iostream>
#include <vector>
#include <queue>
using namespace std;
struct TreeNode
{
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};
// 将二叉树数组转换为链式存储
TreeNode *Construct_Binary_Tree(const vector<int> &vec)
{
    vector<TreeNode *> vecTree(vec.size(), nullptr);
    TreeNode *root = nullptr;
    for (int i = 0; i < vec.size(); i++)
    {
        TreeNode *node = nullptr;
        if (vec[i] != -1)
            node = new TreeNode(vec[i]);
        vecTree[i] = node;
        if (i == 0)
            root = node;
    }
    for (int i = 0; i * 2 + 1 < vec.size(); i++)
    {
        if (vecTree[i] != nullptr)
        {
            vecTree[i]->left = vecTree[i * 2 + 1];
            if (i * 2 + 2 < vec.size())
                vecTree[i]->right = vecTree[i * 2 + 2];
        }
    }
    return root;
}
// 层序遍历打印二叉树
void Print_Binary_Tree(TreeNode *root)
{
    if (root == nullptr)
        return;
    queue<TreeNode *> q;
    q.push(root);
    vector<vector<int>> result;
    while (!q.empty())
    {
        int size = q.size();
        vector<int> vec;
        TreeNode *node;
        for (int i = 0; i < size; i++)
        {
            node = q.front();
            q.pop();
            if (node != nullptr)
            {
                q.push(node->left);
                q.push(node->right);
                vec.push_back(node->val);
            }
        }
        result.push_back(vec);
    }
    for (int i = 0; i < result.size(); i++)
    {
        for (int j = 0; j < result[i].size(); j++)
        {
            cout << result[i][j] << " ";
        }
    }
}
int main()
{
    vector<int> vec = {4, 1, 6, 0, 2, 5, 7, -1, -1, -1, 3, -1, -1, -1, 8};
    TreeNode *root = Construct_Binary_Tree(vec);
    Print_Binary_Tree(root);
    return 0;
}

```

