---
layout: post
title:  "Codility flags solution in Java"
date:   2019-09-03 10:40:00 +0800
categories: Coding
---

本文来源于Codility 的一道题目.[原题传送门](https://app.codility.com/programmers/lessons/10-prime_and_composite_numbers/flags/)


### 题目描述

在给定一个数组中，存在0 - k个peak节点(值大于左右2个邻居的), 目标是将旗子放到peak的位置，并且两个peak的距离(下标差)必须大于等于总旗子数量。


### Brute Force 

先从简单的方案入手，要想知道最多能插入旗子的数量，总共需要2个步骤：
1. 找到数组所有peak, 放入 peak_list.
2. 依次从1到size(peak_list) 尝试是否能够放入指定的旗子.

这个过程可以用以下伪代码来代替，但是注意这只是第一步，还没到正式开始写代码的阶段。


```java

public int solution(int[] A) {
	List<Integer> peaks = getAllPeaks(A);
	int ans = 0;
	for (int i = 1; i < peak.size(); i ++) {
		if (canPutFlags(peaks, i)) {
			ans = i;
		}else{
			break;
		}
	}
	return ans;
}

```

其中`canPutFlags`方法可以依次遍历全有的peak, 判断具体是否满足，如果满足则可以放入旗子。最后判断放入的总旗子是否满足条件。

时间复杂度: `O(N) + O(N) * O(N) = O(N^2)`
	


###  Optimize

整个程序瓶颈在于第二阶段，寻找最大旗子的过程。那么我们看下是否能够优化呢？

尝试寻找规律，如果存在满足条件旗子数为`K`，那么`K - 1` 也一定满足。因此可以使用二分法来减少每次搜索的数量。

尝试从中间位置 MID = PEAK_SIZE / 2，分为2种情况：
1. 如果MID满足，则0 - MID全部满足条件，无需搜索。 
2. 如果MID不满足，则MID - PEAK_SIZE全部不满足，无需搜索。

现在我们的代码变成：

```java

public int solution(int[] A) {
	List<Integer> peaks = getAllPeaks(A);
	return binarySearch(peaks, 1, peaks.size());;
}
```

时间复杂度:  `O(N) + O(N) * O(N * log(N)) = O(N * log(N))`

总体的复杂度下降了一个量级，下面开始真正写代码.

###  Implement

一般来说我们最好将代码按照模块化的方式拆分成若干函数，这样做虽然代码量变多，但是好处多多。

- 可读性好
- 扩展性更好
- 易于测试、问题定位
- 实现简单，只需要专注在一个小问题上。

PS：面试时间不够，可以抓大放小，简单的方法和面试官说一下思路。


```java
 // you can also use imports, for example:
import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {

    public int solution(int[] A) {
        // write your code in Java SE 8
        if (A == null || A.length == 0) {
            return 0;
        }
        // 1. find all peaks.
        List<Integer> peaks = getAllPeaks(A);
        // find max flags, range from 1 - k
        // 2. binary search.
        return binarySearch(peaks);
    }

    private List<Integer> getAllPeaks(int[] A) {
        List<Integer> peaks = new ArrayList();
        for (int i = 1; i < A.length - 1; i++) {
            if (A[i] > A[i + 1] && A[i] > A[i - 1]) {
                peaks.add(i);
            }
        }
        return peaks;
    }

    private Integer binarySearch(List<Integer> peaks) {
        int begin = 1, end = peaks.size();
        while (begin + 1 < end) {
            int mid = begin + (end - begin) / 2;
            if (canPutFlags(peaks, mid)) {
                begin = mid;
            } else {
                end = mid;
            }
        }
        if (canPutFlags(peaks, end)) {
            return end;
        }
        if (canPutFlags(peaks, begin)) {
            return begin;
        }
        return 0;
    }

    public boolean canPutFlags(List<Integer> peaks, int flags) {
        if (peaks.size() == 0) {
            return false;
        }
        int lastIndex = peaks.get(0);
        int usedFlags = 1;
        for (int p = 1; p < peaks.size(); p++) {
            int pIndex = peaks.get(p);
            if (pIndex - lastIndex >= flags) {
                usedFlags++;
                lastIndex = pIndex;
            }
            if (usedFlags == flags) {
                return true;
            }
        }
        // ensure only one peek.
        return usedFlags == flags;
    }
}
```

###  Test

设计一些极端的case，避免产生corner case，例如：
- 没有peak
- 只有1个peak
- peak 的距离间隔为1
- ... 



### 总结

结果查看： [https://app.codility.com/demo/results/trainingKNHF4F-8UV/](https://app.codility.com/demo/results/trainingKNHF4F-8UV/)








