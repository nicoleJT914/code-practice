对于一个元素各不相同且按升序排列的有序序列，请编写一个算法，创建一棵高度最小的二叉查找树。

给定一个有序序列int[] vals,请返回创建的二叉查找树的高度。

只计算高度
```java
import java.util.*;

public class MinimalBST {
    public int buildMinimalBST(int[] vals) {
        return buildMinimalBST(0, vals.length-1);
    }
    public int buildMinimalBST(int lo, int hi) {
        if (hi < lo) return 0;
        int mid = lo + (hi-lo)/2;
        return Math.max(buildMinimalBST(lo, mid-1), buildMinimalBST(mid+1, hi)) + 1;
    }
}
```

建树
```java
import java.util.*;

public class MinimalBST {
    public TreeNode buildMinimalBST(int[] vals) {
        return buildMinimalBST(vals, 0, vals.length-1);
    }
    public TreeNode buildMinimalBST(int[] arr, int lo, int hi) {
        if (hi < lo) return null;
        int mid = lo + (hi-lo)/2;
        TreeNode n = new TreeNode(arr[mid]);
        n.left = buildMinimalBST(arr, lo, mid-1);
        n.right = buildMinimalBST(arr, mid+1, hi);
        return n;
    }
}
```
