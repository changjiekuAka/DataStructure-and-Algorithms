# Mosrris

```c++
void func(Node* head)
{
	Node* cur = head;
    Node* mostRight = nullptr;
    while(cur!=nullptr)
    {
        mostRight = cur->left;
        if(mostRight != nullptr)
        {
        	while(mostRight->right != nullptr && mostRight->right != cur)
        	{
            	mostRight = mostRight->right;
        	}	
        
        	if(mostRight->right == nullptr)
        	{
        		cout << cur->val;
            	mostRight->right = cur;
            	cur = cur->left;
            	continue;
        	}
        	else
        	{
            	mostRight->right = nullptr;
        	}
        }
        cur = cur->right;
    }
}
```

```
void func(Node* head)
{
	Node* cur = head;
    Node* mostRight = nullptr;
    while(cur!=nullptr)
    {
        mostRight = cur->left;
        if(mostRight != nullptr)
        {
        	while(mostRight->right != nullptr && mostRight->right != cur)
        	{
            	mostRight = mostRight->right;
        	}	
        
        	if(mostRight->right == nullptr)
        	{
        		cout << cur->val;
            	mostRight->right = cur;
            	cur = cur->left;
            	continue;
        	}
        	else
        	{
            	mostRight->right = nullptr;
        	}
       }
       else
       {
       		cout << cur->val;
       }
       cur = cur->right;
    }
}
```

