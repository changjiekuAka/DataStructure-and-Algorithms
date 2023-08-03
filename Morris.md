# Mosrris

```c++
void func(Node* head)
{
	Node* cur = head;
    Node* mostRight = nullptr;
    while(cur!=nullptr)
    {
        mostRight = cur->left;
        
        while(mostRight->right != nullptr && mostRight->right != cur)
        {
            mostRight = mostRight->right;
        }
        
        if(mostRight->right == nullptr)
        {
            mostRight->right = cur;
            cur = cur->left;
            continue;
        }
        else
        {
            mostRight->right = nullptr;
        }
        
        cur = cur->right;
    }
}
```

