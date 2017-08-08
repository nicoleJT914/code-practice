输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

```java
import java.util.*;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        if (k > input.length) return res;
        Arrays.sort(input);
        for (int i=0;i<k;i++) {
            res.add(input[i]);
        }
        return res;
    }
}
```

```java
import java.util.*;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList<Integer>();
        if (k > input.length || k<=0) return res;
        for (int i=0; i<k; i++) {
            res.add(input[i]);
        }
        Collections.sort(res);
        for (int i=k; i<input.length; i++) {
            if (input[i] < res.get(res.size()-1)) {
                res.set(res.size()-1, input[i]);
                Collections.sort(res);
            }
        }
        return res;
    }
}
```

基于堆
```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.PriorityQueue;
public class Solution {
    public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
        ArrayList<Integer> res = new ArrayList<>();
        int len = input.length;
        if (k > len || k == 0) {
            return res;
        }
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(k, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2.compareTo(o1);
            }
        });
        for (int i=0; i<len; i++) {
            if (maxHeap.size() != k) {
                maxHeap.offer(input[i]);
            }else if (maxHeap.peek() > input[i]) {
                maxHeap.poll();
                maxHeap.offer(input[i]);
            }
        }
        for (int integer: maxHeap) {
            res.add(integer);
        }
        return res;
    }
}
```
