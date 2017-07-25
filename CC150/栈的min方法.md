设计一个栈，除push和pop外，还支持min方法，返回栈元素中的最小值。min方法的时间复杂度必须为O(1)。
 
思路1：设计一个带最小值的栈，每次记录最小值。
```java
public class NodeWithMin {
    int value;
    int min;
    NodeWithMin(int v, int min) {
        this.value = v;
        this.min = min;
    }
}
public class StackWithMin extends Stack<NodeWithMin> {
    public void push(int value) {
        int newMin = Math.min(value, min());
        super.push(new NodeWithMin(value, newMin));
    }
    public int min() {
        if (this.isEmpty()) {
            // 错误值
            return Integer.MAX_VALUE;
        } else {
            return this.peek().min;
        }
    }
}
```
思路2：将最小值重新存到另一个栈中。
```java
public class StackWithMin2 extends Stack<Integer> {
    Stack<Integer> s2;
    public StackWithMin2() {
        s2 = new Stack<Integer>();
    }

    public void push(int value) {
        if (value <= min()) {
            s2.push(value);
        }
        super.push(value);
    }

    public Integer pop() {
        int value = super.pop();
        if (value == min()) {
            s2.pop();
        }
        return value;
    }

    public int min() {
        if (s2.isEmpty()) {
            return Integer.MAX_VALUE;
        }else {
            return s2.peek();
        }
    }
}
```
