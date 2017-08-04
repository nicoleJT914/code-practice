有一个XxY的网格，一个机器人只能走格点且只能向右或向下走，要从左上角走到右下角。请设计一个算法，计算机器人有多少种走法。
给定两个正整数int x,int y，请返回机器人的走法数目。保证x＋y小于等于12。

这里定义只能走格点，即2*2的网格只有2种走法

思路是x*y的格点，从左上走到右下要向右x-1步，向下y-1步，即从x+y-2中选x-1

定理：n选r ==》(n)!/(r!(n-r)!)
```java
import java.util.*;

public class Robot {
    public int countWays(int x, int y) {
        if (x == 1 || y == 1) return 1;
        else {
            x = x-1;
            y = y-1;
            int[] list = new int[x+y];
            list[0] = 1;
            for (int i=1;i<x+y;i++) {
                list[i] = (i+1) * list[i-1]; 
            }
            int res = list[x+y-1]/(list[x-1]*list[y-1]);
            return res;
        }
    }
}
```

```java
import java.util.*;
// 递归
public class Robot {
    public int countWays(int x, int y) {
        if (x <= 0 || y <= 0) return 0;
        if (x == 1 || y == 1) return 1;
        return countWays(x-1,y)+countWays(x,y-1);
    }
}
```
