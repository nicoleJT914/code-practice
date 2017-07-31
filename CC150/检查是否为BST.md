请实现一个函数，检查一棵二叉树是否为二叉查找树。
给定树的根结点指针TreeNode* root，请返回一个bool，代表该树是否为二叉查找树。

中序遍历 
```java
import java.util.*;

/*
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;
    public TreeNode(int val) {
        this.val = val;
    }
}*/
public class Checker {
    public boolean checkBST(TreeNode root) {
        ArrayList<Integer> arr = new ArrayList<>();
        checkBST(root, arr);
        for (int i=1; i<arr.size(); i++) {
            if (arr.get(i) < arr.get(i-1)) return false;
        }
        return true;
    }
    private void checkBST(TreeNode x, ArrayList<Integer> arr) {
        if (x == null) return;
        checkBST(x.left, arr);
        arr.add(x.val);
        checkBST(x.right, arr);
    }
}
```

中序遍历改进
```java
public class Checker {
    public int oldVal = Integer.MIN_VALUE;
    public boolean checkBST(TreeNode root) {
        if (root == null) return true;
        if (!checkBST(root.left)) return false;
        if (root.val < oldVal) return false;
        oldVal = root.val;
        if (!checkBST(root.right)) return false;
        return true;
    }
}
```

根节点大于左子树所有值，小于右子树所有值
```java
public class Checker {
    public boolean checkBST(TreeNode root) {
        return checkBST(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
    private boolean checkBST(TreeNode x, int min, int max) {
        if (x == null) return true;
        if (x.val < min || x.val >= max) return false;
        if (!checkBST(x.left, min, x.val) || !checkBST(x.right, x.val, max)) return false;
        return true;
    }
}
```
