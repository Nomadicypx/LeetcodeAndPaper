## 前K个高频单词

* 前K个是关键信息，这种题型需要我们用到大根堆或者小根堆
* 这个题目最简单的想法是使用一个map结构，最后将map中的元素按照value的大小进行排序即可，这种思路局限的地方是后面的排序行为，由于我们只需要前面的K个元素，可以不需要进行对整个队列的排序，这个时候引入大根堆或者小根堆可以（即引入优先队列）减小复杂度
* 总的来说这是一个训练STL的题：主要组合是Map+PriorityQueue

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String,Integer> map = new HashMap<String,Integer>();
        for(String word:words){
            map.put(word,map.getOrDefault(word,0)+1);
        }//建立完整hashmap


        PriorityQueue<Map.Entry<String,Integer>> queue = new PriorityQueue<Map.Entry<String,Integer>>(
            new Comparator<Map.Entry<String,Integer>>(){
                @Override
                public int compare(Map.Entry<String,Integer> arg0,Map.Entry<String,Integer>arg1){
                    return arg0.getValue()==arg1.getValue()?arg1.getKey().compareTo(arg0.getKey()):arg0.getValue()-arg1.getValue();
                }
            }
        );
        for(Map.Entry<String,Integer> e:map.entrySet()){
            queue.offer(e);
            if(queue.size()>k){
                queue.poll();
            }
        }
        List<String> list = new ArrayList<String>();
        while(!queue.isEmpty()){
            list.add(queue.poll().getKey());
        }
        Collections.reverse(list);
        return list;
    }
}
```

* 需要注意的内容,Map.Entry<String,Integer>的结构是Map中存入的单个元素，作为有限队列的存储单元，其次因为最后的结果需要倒序，所以在优先队列的比较器里需要先将同value的key倒序一下使用的是arg1.getKey().compareTo(arg0.getKey)！！！