# Leetcode 题解

## day001

```
146. LRU缓存机制
题目描述：
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

示例：
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得关键字 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得关键字 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4

进阶:
你是否可以在 O(1) 时间复杂度内完成这两种操作？
```



```java
// 思路

```















```
11. 盛最多的水的容器
给你 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。

说明：你不能倾斜容器，且 n 的值至少为 2。
```



```java
// 暴力解法，遍历两次，时间复杂度为O(N^2)
public int maxArea(int[] nums) {
    int max = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            max = Math.max(max, (j - i) * Math.min(nums[i] - nums[j]));
        }
    }
    return max;
}


// 双端向内收敛，一次遍历，时间复杂度O(N)
public int maxArea2(int[] nums) {
    int max = 0;
    // 双指针的写法，要记得滚瓜烂熟！
    for (int i = 0, j = nums.length - 1; i < j; ) {
        // 短的那一头往中间靠拢，nums[i]小的话，i++；nums[j话，j--。
        int minHeight = nums[i] < nums[j] ? nums[i++] : nums[j--];
        max = Math.max(max, (j - i + 1) * minHeight);
    }
    return max;
}

// 另一种写法，i++；j--
public int maxArea3(int[] nums) {
    int max = 0;
    for (int i = 0, j = nums.length - 1; i < j; ) {
        max = Math.max(max, (j - i + 1) * Math.min(nums[i], nums[j]));
        if (nums[i] < nums[j]) {
            i++;
        } else {
            j--;
        }
    }
}

// 
public int maxArea4(int[] nums) {
    int max = 0;
    int left = 0, right = nums.length - 1;
    while (left < right) {
        max = Math.max(max, (j - i + 1) * Math.min(nums[left], nums[right]));
        if (nums[left] < nums[right]) {
            left++;
        } else {
            right++;
        }
    }
}
```





```
283. 移动零
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]

说明:
必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。
```



```java
// 暴力解法
public int[] moveZeroes(int[] nums) {
    
}


// 思路：数组变换问题
public int[] moveZeroes2(int[] nums) {
    
}
```











第20题：有效的括号

valid-parentheses——20（有效的括号）

```java
// 暴力解法，遍历

```



```java
// 思路：使用栈，遇到左括号就压栈，遇到右括号就与栈顶比对，为一对的话就弹栈
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();
    char[] char = s.stringtoArray();
    for (int i = 0; i < char.length; i++) {
        if (char[i] == '(')
            stack.push(')');
        else if (char[i] == "[")
            stack.push(']');
        else if (char[i] == '{')
            stack.push('}');
        else if (stack.isEmpty() || stack.pop() != c)
            return false;
    }
    return stack.isEmpty();
}
```



国际站优解



min-stack













largeset-rectangle-in-hisogram









sliding-window-maximun











design-circular-deque













trapping-rain-water







group-anagram, two sum

第242题：有效的字母异位词

Valid anagram——

```java
// 暴力解法

```



```java
// 思路：通过map记录一个字母出现的次数，比较计数的差异。两遍哈希表
```



第70题：爬楼梯

climbing-stairs

```java
// 直接递归解决
public int climbStairs(int n) {
    climb_Stairs(0, n);
}

public int climb_Stairs(int i, int n) {
    if (i > n) {
        return 0;
    }
    if (i == n) {
        return 1;
    }
    return climb_Stairs(i + 1, n) + climb_Stairs(i + 2, n);
}
```





```java
// 思路：记忆化递归

```







```java
// 动态规划

```









第22题：括号生成



generate-parentheses

```java
// 

```

