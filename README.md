# 什么时候需要用虚拟头结点？  
总结一下：当需要创造一条新链表的时候，可以使用虚拟头结点简化边界情况的处理。

# 遇到一道二叉树的题目时的通用思考过程是：  
&emsp;&emsp;1、是否可以通过遍历一遍二叉树得到答案？如果可以，用一个 traverse 函数配合外部变量来实现。  
&emsp;&emsp;2、是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案？如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。  
&emsp;&emsp;3、无论使用哪一种思维模式，你都要明白二叉树的每一个节点需要做什么，需要在什么时候（前中后序）做。  

&emsp;&emsp;一旦你发现题目和子树有关，那大概率要给函数设置合理的定义和返回值，在后序位置写代码了。

&emsp;&emsp;动态规划的核心思想就是穷举求最值，但需要熟练掌握递归思维，只有列出正确的「状态转移方程」，才能正确地穷举。  
&emsp;&emsp;而且，需要判断算法问题是否具备「最优子结构」，是否能够通过子问题的最值得到原问题的最值。  
&emsp;&emsp;另外，动态规划问题存在「重叠子问题」，如果暴力穷举的话效率会很低，所以需要使用「备忘录」或者「DP table」来优化穷举过程，避免不必要的计算。   
&emsp;&emsp;重叠子问题、最优子结构、状态转移方程就是动态规划三要素，但是在实际的算法问题中，写出状态转移方程是最困难的。

# 动态规划框架
![image](https://user-images.githubusercontent.com/90192841/227175873-c080b027-14b7-41ee-b5de-fe3930518d02.png)
### 动态规划典型题目（未解决）
322
# 递归算法的时间复杂度怎么计算？
就是用子问题个数乘以解决一个子问题需要的时间。

# 回溯算法的框架
![image](https://user-images.githubusercontent.com/90192841/227175598-13a64c58-47a9-40a3-8c92-464fcab145cd.png)  
回溯算法时间复杂度不可能低于 O(N!)，因为穷举整棵决策树是无法避免的。这也是回溯算法的一个特点，不像动态规划存在重叠子问题可以优化，回溯算法就是纯暴力穷举，复杂度一般都很高。
### 解决一个回溯问题，实际上就是一个决策树的遍历过程，站在回溯树的一个节点上，你只需要思考 3 个问题：
1、路径：也就是已经做出的选择。  
2、选择列表：也就是你当前可以做的选择。  
3、结束条件：也就是到达决策树底层，无法再做选择的条件。
# 回溯算法解决所有排列/组合/子集问题
### 形式一、元素无重不可复选，即 nums 中的元素都是唯一的，每个元素最多只能被使用一次  
&emsp;&emsp;子集：使用 start 参数控制树枝的遍历，避免产生重复的子集；同时用 track 记录根节点到每个节点的路径的值，同时在前序位置把每个节点的路径值收集起来，完成回溯树的遍历就收集了所有子集  
&emsp;&emsp;组合：遍历同子集，选择时在base case加上相应条件即可  
&emsp;&emsp;排列：使用used 数组标记已经在路径上的元素，避免重复选择  
### 形式二、元素可重不可复选，即 nums 中的元素可以存在重复，每个元素最多只能被使用一次  
&emsp;&emsp;子集/组合：将nums进行排序；使用 start 参数控制树枝的遍历，避免产生重复的子集；使用nums[i] == nums[i - 1]进行剪枝（剪枝逻辑：值相同的相邻树枝，只遍历第一条）  
&emsp;&emsp;排列：将nums进行排序；使用used 数组标记已经在路径上的元素，避免重复选择；使用nums[i] == nums[i - 1] and !used[i - 1]进行剪枝（或使用preNum记录前一条树枝的值，使用nums[i] == preNum进行剪枝）  
### 形式三、元素无重可复选，即 nums 中的元素都是唯一的，每个元素可以被使用若干次  
&emsp;&emsp;子集/组合：在元素无重不可复选的子集/组合问题中，使用start参数控制树枝的遍历，下一层回溯树从i + 1开始，在元素无重可复选问题中，只需要使下一层回溯树从i开始就行  
&emsp;&emsp;排列：在元素无重不可复选的基础上，去除uesd数组操作即可  
# DFS算法、BFS算法
### DFS算法就是回溯算法  
### BFS算法核心思想：  
&emsp;&emsp;就是一幅[图]，让你从一个起点start，走到终点end，问最短路径。一般来说，我们写BFS算法都是用[队列]这种数据结构，每次将一个节点周围的所有节点加入队列。  
&emsp;&emsp;BFS相对DFS的最主要的区别是：BFS找到的路径一定是最短的，但代价就是空间复杂度可能比DFS大很多  
![image](https://user-images.githubusercontent.com/90192841/227970145-a61a0d99-0b55-4c73-8165-d818010b4bc1.png)  
# 二分搜索算法
![image](https://user-images.githubusercontent.com/90192841/229037250-dd31eb78-0302-430c-8b57-6db1b868c0f1.png)  
### 第一类：普通二分查找框架
![image](https://user-images.githubusercontent.com/90192841/229037637-4fff056f-f743-4d60-9396-2a12fe92bfef.png)  
### 一些细节
&emsp;&emsp;1、计算 mid 时需要防止溢出，代码中left + (right - left) / 2 就和 (left + right) / 2 的结果相同，但是有效防止了 left 和 right 太大，直接相加导致溢出的情况。  
&emsp;&emsp;2、while 循环的条件中是 <= 而不是 < 。算法使用的是[left, right] 两端都闭的区间，while(left <= right) 的终止条件是 left == right + 1，如[3, 2]，不会漏掉情况  
&emsp;&emsp;3、left = mid + 1，right = mid - 1  
&emsp;&emsp;4、算法缺陷：例如给出有序数组 nums = [1,2,2,2,3]，target 为 2，此算法返回的索引为 2，没错。但是如果我想得到 target 的左侧边界，即索引 1，或者我想得到 target 的右侧边界，即索引 3，这样的话此算法是无法处理的。  
### 第二类：寻找左侧边界的二分搜索框架
![image](https://user-images.githubusercontent.com/90192841/229041745-db7737be-5aac-4244-bf52-f94a7c28f72b.png)  
### 一些细节
&emsp;&emsp;1、right = len(nums)，故while 中是 < 而不是 <=，搜索的是[left, right)左闭右开区间，终止的条件是 left == right，此时搜索区间 [left, left) 为空，所以可以正确终止。  
&emsp;&emsp;2、没有返回 -1 的操作，在返回的时候额外判断一下 nums[left] 是否等于 target 就行了，如果不等于，就说明 target 不存在。  
&emsp;&emsp;3、left = mid + 1，right = mid，因为「搜索区间」是 [left, right) 左闭右开。  
&emsp;&emsp;4、nums[mid] == target 时不要立即返回，而是缩小「搜索区间」的上界 right，在区间 [left, mid) 中继续搜索，即不断向左收缩，保证搜索到左侧边界。  
&emsp;&emsp;5、若right = len(nums) - 1 (同普通二分算法),也可以，只是 while 中需要用 <= ,且nums[mid] == target时right = mid - 1，最后返回部分的代码：  
&emsp;&emsp;![image](https://user-images.githubusercontent.com/90192841/229045077-d59ad844-2acb-4280-a937-279691515234.png)  
# 第三类：寻找右侧边界的二分查找框架
![image](https://user-images.githubusercontent.com/90192841/229045561-089ae891-58ec-40c1-9a19-f872283450b3.png)  
### 一些细节
&emsp;&emsp;1、当 nums[mid] == target 时，不要立即返回，而是增大「搜索区间」的左边界 left，使得区间不断向右靠拢，达到锁定右侧边界的目的。  
&emsp;&emsp;2、最后返回 left - 1 ，因为 while 循环的终止条件是 left == right，所以 left - 1 同 right - 1 ，至于为什么要减一，关键在锁定右边界(nums[mid] == target)时的这个条件判断 left = mid + 1 (即mid = left - 1)，故 while 循环结束时，nums[left] 一定不等于 target ，而 nums[left - 1] 可能是 target。  
&emsp;&emsp;3、返回部分的代码：  
&emsp;&emsp;![image](https://user-images.githubusercontent.com/90192841/229047062-e77755fc-9fdb-4824-a612-f57a361fbc9e.png)  
&emsp;&emsp;4、right = len(nums) - 1 时代码框架：  
&emsp;&emsp;![image](https://user-images.githubusercontent.com/90192841/229047637-9a986776-6ec2-48b6-8e6b-a6e2adf62de3.png)  
# 滑动窗口算法
![image](https://user-images.githubusercontent.com/90192841/229101192-3d374067-581f-40e6-9d69-8f13f3197117.png)  
### 滑动窗口算法框架
![image](https://user-images.githubusercontent.com/90192841/229102178-d00b91a0-147f-42b5-ba02-7f09a1265488.png)  
### 前置初始化：
&emsp;&emsp;from collections import defaultdict + window, need = defaultdict(int), defaultdict(int)(Python)  
&emsp;&emsp;#include <unordered_map> + unordered_map<char, int> need, window;(C++)  
&emsp;&emsp;left = 0, right = 0, valid = 0, length = float('inf')  
### 算法主要需要思考以下几个问题：
&emsp;&emsp;1、什么时候应该移动 right 扩大窗口？窗口加入字符时，应该更新哪些数据？  
&emsp;&emsp;2、什么时候窗口应该暂停扩大，开始移动 left 缩小窗口？从窗口移出字符时，应该更新哪些数据？  
&emsp;&emsp;3、我们要的结果应该在扩大窗口时还是缩小窗口时进行更新？  
