# Prefix tree

### 前缀树实现

```java
class Node
{
  	public int pass;
    public int end;
    public Node[] nexts;
  	/******也可以用哈希表******/
    public Node()
    {
       	pass = 0;
        end = 0;
        nexts = new Node[26];
    }
};

class Tris
{
    private Node root;
    public Tris(){root = new Node(); }
    
    public void Insert(string str)
    {
        if(str == null)
        {
            return;
        }
        
        char[] chs = str.toCharArray();
        Node node = root;
        node.pass++;
        int index = 0;
 		for(int i = 0;i < charr.size(); i++)
        {
            index = chs[i] - 'a';
            if(node.nexts[index] == null)
            {
                node.nexts[index] = new Node();
            }
            node = node.nexts[index];
            node.pass++;
        }
        node.end++;
    }
    
    public void Desert(string str)
    {
        if(!Search(str)) return;
        
        char[] chs = str.toCharArray();
        Node node = root;
        int index = 0;
        node.pass--;
        for(int i = 0;i < chs.size(); i++)
        {
            index = chs[i] - 'a';
            if(--node.nexts[index].pass == 0)
            {
                node.nexts[index] = null;
                return;
                /******c++需要手动遍历释放节点******/
            }
            node = node.nexts[index];
        }
        node.end--;
    }
    
    public boolean Search(string str)
    {
        if(str == null) return true;
        
        char[] chs = str.toCharArray();
        Node node = root;
        int index = 0;
        for(int i = 0;i < chs.size(); i++)
        {
            index = chs[i] - 'a';
            if(node.nexts[index] == null) return false;
            node = node.nexts[index];
        }
        return node.end > 0;
    }
    /******查找有多少以str为前缀的字符串******/
    public int SearchPre(string str)
    {
        if(str == null) return 0;
        
        Node node = root;
        int index = 0;
        char[] chs = str.toCharArray();
        
        for(int i = 0;i < chs.size();i++)
        {
            index = chs[i] - 'a';
            if(node.nexts[index] == null) return 0;
            node = node.nexts[index];
        }
        return node.pass;
    }
}
```

