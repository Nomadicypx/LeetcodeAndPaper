# 实现trie(前缀树)

> 这个题目就是一个构建多分叉树结构的题目

* 要注意前缀和搜寻与插入的关系
* 插入的字符末尾节点需要添加一个flag表示这个词已经插入过了
* 搜寻的时候需要验证最后一个单元的flag是否是true表示是已经插入的节点，如果是prefix的情况，那么可以不用管
* 分支采用hashmap解决，key代表分支的名字，node建议一个分支节点

```java
class Node{
    public char val;
    public Map<Character,Node> map;
    public int flag = -1;
    public Node(char val){
        this.val = val;
        this.map = new HashMap<Character,Node>();
    }
}
class Trie {


    Node root;

    /** Initialize your data structure here. */
    public Trie() {
        root = new Node('A');//根节点
        root.flag = -2;
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        int i = 0;
        int len = word.length();
        Node pos = this.root;
        while(i<len){
            char val = word.charAt(i);
            
            if(pos.map.containsKey(val)){
                pos = pos.map.get(val);
            }
            else{
                Node temp = new Node(val);
                pos.map.put(val, temp);                
               pos = temp;
            }
            i++;
        }
        pos.flag = 0;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        int i = 0;
        int len = word.length();
        Node pos = root;    
        while(i<len){
            char val = word.charAt(i);
            
            if(pos.map.containsKey(val)){
                pos = pos.map.get(val);
                System.out.println(val);
            }
            else{
                break;
            }
            i++;
        }
        if(i==len&&pos.flag==0){
            return true;
        }
        else{
            return false;
        }
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        int i = 0;
        int len = prefix.length();
        Node pos = this.root;    
        while(i<len){
            char val = prefix.charAt(i);
            
            if(pos.map.containsKey(val)){
                pos = pos.map.get(val);
            }
            else{
                break;
            }
            i++;
        }
        if(i==len){
            System.out.println(i);
            return true;
        }
        else{
            return false;
        }

    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

