有一些数的素因子只有3、5、7，请设计一个算法，找出其中的第k个数。
给定一个数int k，请返回第k个数。保证k小于等于100。

```java
import java.util.*;

public class KthNumber {
    public int findKth(int k) {
        if (k < 0) return 0;
        int val = 0;
        Queue<Integer> que3 = new LinkedList<Integer>();
        Queue<Integer> que5 = new LinkedList<Integer>();
        Queue<Integer> que7 = new LinkedList<Integer>();
        que3.add(1);
        
        for (int i=0; i<=k; i++) {
            int v3 = que3.size() > 0 ? que3.peek() : Integer.MAX_VALUE;
            int v5 = que5.size() > 0 ? que5.peek() : Integer.MAX_VALUE;
            int v7 = que7.size() > 0 ? que7.peek() : Integer.MAX_VALUE;
            val = Math.min(v3, Math.min(v5, v7));
            if (val == v3) {
                que3.remove();
                que3.add(3*val);
                que5.add(5*val);
            }else if (val == v5) {
                que5.remove();
                que5.add(5*val);
            }else if(val == v7) {
                que7.remove();
            }
            que7.add(7*val);
        }
        return val;
    }
}
```
