### Jump Game

![](Jump Game.assets/屏幕截图 2022-01-15 122825.png)

Jump Game的介绍，就是判断是否能够到达最终的目的地，每一个表示nums[i]可以跳跃的步数

#### 方法1：

##### 动态规划

```python
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        dp = [0]*(n)
        dp[0] = nums[0]
        for i in range(n):
            dp[i-1]
        for i in range(1,n):
            for j in range(i):
                if dp[j] == 1:
                    if nums[j] >= i-j:
                        dp[i] = 1
                        break
        if dp[-1] == 1:
            return True
        else:
            return False
```

在每个dp中装有是否能到达的信息，能则是设置为1，不能设置为0，这意思是在dp中我们每一个值都得进行遍历所以会使得整个时间复杂度会到达$O(n^2)$,因为对于某一个dp值，我们要判断之前的的值是否能够到达目前的位置，如果能到达，我们就设定为1，但是一般这种复杂度不能通过时间限制

#### 方法2：

##### 贪心

其实对于这样的问题，贪心是能保证找到全局最优解的，只要我们能保证在某一格中能够到达同时他能跳的步数超过最后的index，这样就能在将复杂度降为$O(n)$

```python
    def canJump(self, nums: List[int]) -> bool:
        n = len(nums)
        max_length = 0
        for i in range(n):
            if i <= max_length:
                max_length = max(max_length,nums[i]+i)
            if max_length >= n-1:
                return True
        return False

```

能够保证速度，同时空间复杂度为$O(1)$

上述都为自己写的代码，具体可参考

[跳跃游戏 - 跳跃游戏 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/jump-game/solution/tiao-yue-you-xi-by-leetcode-solution/)

