# 快速排序练习

> 今天的题目想用一下手写快速排序算法，发现自己虽然知道快排是什么但是没有形成肌肉记忆，现在重新练习一下，快速排序的写法

```c++
# include<iostream>
using namespace std;
int ArrayPos(int*,int,int);
int main(){
    int array[7] = {28,4,6,99,12,55,7};
	quickSort(array,0,6);
}
int ArrayPos(int []nums,int left,int right){
    int pos = nums[left] ;
    int i = left;
    int j = right;
	while(i<j){
                while(nums[j]>pos&&j>i){//这里需要检测j>i是否成立，防止j碰到常数数列越界
            j--;
        }
        if(i<j){//牢记，每次坐标发生改动的时候都要盘带按是否i<j,因为这个时候可以i==j成立
            nums[i] = nums[j];
            i++;//这里要++因为有可能换过来的是一个与pos相等的值，不++永远卡在这里
        }
        while(nums[i]<pos&&j>i){
            i++;
        }
        if(i<j){
            nums[j] = nums[i];
            j--;
        }
    }
    nums[i] = pos;
    return i;//最后i和j肯定是相等的
}
void quickSort(int[]nums,int left,int right){
    if(left<right){
        int i = ArrayPos(nums,left,right);
        quickSort(nums,i+1,right);
        quickSort(nums,left,i-1);
    }
}
```

* 这里写一个合并在一起的写法

```c++
# include<iostream>
using namespace std;
void quickSort(int nums[],int,int)
int main(){
	int array[7] = {28,4,6,99,12,55,7};
	quickSort(array,0,6);
}
void quickSort(int[]nums,int left,int right){
    if(left<right){
        int i = left;
        int j = right;
        int pos = nums[l];
        while(i<j){
            while(nums[j]>pos&&j>i)
            j--;
            if(j>i){
                nums[i]=nums[j];
                i++;
            }
            while(nums[i]<pos&&j>i)
                i++;
            if(j>i){
                nums[j]=nums[i];
                j--;
            }
        }
        nums[i]=pos;
        quickSort(nums,left,i-1);
        quickSort(nums,i+1,right);
    }
}
```

* 再写一遍

```c++
void quickSort(int nums[],int left,int right){
	if(left<right){
		int i = left;
		int j = right;
		int pos = nums[i];
		while(i<j){
            while(i<j&&nums[j]>pos){
                j--;
            }
            if(i<j){
                nums[i++]=nums[j];
            }
            while(i<j&&nums[i]<pos){
                i++;
            }
            if(i<j){
                nums[j--]=nums[i];
            }
        }
		nums[i]=pos;
		quickSort(nums,left,i-1);
		quickSort(nums,i+1,right);
	}
}
```

* 再写一遍

```c++
void quickSort(int nums[],int left,int right){
	if(left<right){
		int i = left;
		int j = right;
		int pos = nums[i];
		while(i<j){
			while(j>i&&nums[j]>pos)
				j--;
            if(i<j)
            	nums[i++]=nums[j];
            while(j>i&&nums[i]<pos)
            	i++;
            if(i<j)
            	nums[j--]=nums[i];
		}
		nums[i]=pos;
		quickSort(nums,left,i-1);
		quickSort(nums,i+1,right);
	}
}
```

