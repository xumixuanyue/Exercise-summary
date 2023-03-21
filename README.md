什么时候需要用虚拟头结点？总结一下：当需要创造一条新链表的时候，可以使用虚拟头结点简化边界情况的处理。

综上，遇到一道二叉树的题目时的通用思考过程是：  
1、是否可以通过遍历一遍二叉树得到答案？如果可以，用一个 traverse 函数配合外部变量来实现。  
2、是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案？如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。  
3、无论使用哪一种思维模式，你都要明白二叉树的每一个节点需要做什么，需要在什么时候（前中后序）做。  
一旦你发现题目和子树有关，那大概率要给函数设置合理的定义和返回值，在后序位置写代码了。

动态规划的核心思想就是穷举求最值，但需要熟练掌握递归思维，只有列出正确的「状态转移方程」，才能正确地穷举。  
而且，需要判断算法问题是否具备「最优子结构」，是否能够通过子问题的最值得到原问题的最值。  
另外，动态规划问题存在「重叠子问题」，如果暴力穷举的话效率会很低，所以需要使用「备忘录」或者「DP table」来优化穷举过程，避免不必要的计算。   
重叠子问题、最优子结构、状态转移方程就是动态规划三要素，但是在实际的算法问题中，写出状态转移方程是最困难的。

# 自顶向下递归的动态规划
def dp(状态1, 状态2, ...):  
    for 选择 in 所有可能的选择:  
        # 此时的状态已经因为做了选择而改变  
        result = 求最值(result, dp(状态1, 状态2, ...))  
    return result

# 自底向上迭代的动态规划
# 初始化 base case
dp[0][0][...] = base case  
# 进行状态转移
for 状态1 in 状态1的所有取值：  
    for 状态2 in 状态2的所有取值：  
        for ...  
            dp[状态1][状态2][...] = 求最值(选择1，选择2...)  
