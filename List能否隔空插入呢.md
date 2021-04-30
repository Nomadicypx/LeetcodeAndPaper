# List能否隔空插入呢

> 答案是不行

* 每次插入的默认情况是尾插入，如果有index首先会判断index和size的大小，如果index>size会报错也就是说每次插入元素的时候元素们都是紧靠再一起的，只有当index<size的时候，list会进行插入此后的元素顺位后移
* 替换的情况
  * list.set(index,value)即可
  * list.replaceAll(org,dst)
* 顺便提一下数组tolist的方法
  * nums[].aslist这个方法得到的list是不能扩容的

