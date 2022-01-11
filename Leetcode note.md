# Array: 
      如果有了暴力解法的想法，可以尝试的第一步优化总是sort at first

      避免duplicate，可以使用set作为结果容器，会自动消除duplicate
      找数或者对比数时，尽量进行反向思维（先找后放入容器）
      
      找最大减：max, min更新， greedy method
      找缺失值：用set(...) in; 求和; XOR
      找最大subarray: Greedy, DP
      Hash table - switch key and value pair

      三数sum：1. sort整个数列，设当前i，对剩余数组进行双指针找sum <- 简化成二数sum问题, 
                 TC: O(n**2) -> 找两数sum O(n) for n times, 存储array O(nlogn) -> O(nlogn + n**2)
                 SC: O(n) -> O(logn) ~ O(n)
              2. hash table, 同1方法，sort整个数列，设立当前i，然后对剩余的数组建立dictionary来找到target,
                 TC: O(n**2) -> 建立hash table O(n) for n times, 存储array O(nlogn) -> O(nlogn + n**2)
                 SC: O(n) for the hashset
                 *如果不sort数列也可以，但为了确保没有duplicate需要对结果进行tuple(sorted((a,b,c))处理

      252. Meeting Rooms |, 253. Meeting Rooms ||:
      Interval问题, 首选排序，然后对比 (overlapping可以通过开始时间排序， Non-overlapping可以通过结束时间排序): 大致思路：
      Sort intervals/pairs in increasing order of the start position.
      Scan the sorted intervals, and maintain an "active set" for overlapping intervals. At most times, we do not need to use an explicit set to store them. Instead, we just need to maintain several key parameters, e.g. the number of overlapping intervals (count), the minimum ending point among all overlapping intervals (minEnd).
      If the interval that we are currently checking overlaps with the active set, which can be characterized by cur.start > minEnd, we need to renew those key parameters or change some states.
      If the current interval does not overlap with the active set, we just drop current active set, record some parameters, and create a new active set that contains the current interval.
      
      解法1：Heapq最小树，通过对比meeting结束和新meeting开始时间，老结束时间 < 新开始时间： pop掉老结束时间，存入新结束时间，房间续上了； 反之，不pop老结束时间，push进新结束时间，安排新房间
      # Heap solution
      # class Solution:
      #     def minMeetingRooms(self, intervals: List[List[int]]) -> int:
      #         if not intervals:
      #             return 0
            
      #         rooms = []
      #         intervals.sort(key=lambda x: x[0])
      #         heapq.heappush(rooms, intervals[0][1])
            
      #         for i in intervals[1:]:
      #             if rooms[0] <= i[0]:
      #                 heapq.heappop(rooms)
      #             heapq.heappush(rooms, i[1])
      #         return len(rooms)
      解法2：双指针，分开思考开始和结束时间，分别排序，然后拿每一个结束时间与开始时间进行对比，如果结束时间大于开始时间，则增加房间，反之代表当前meeting已经结束，结束时间指针移至下一个。
      # Two pointers
      class Solution:
      def minMeetingRooms(self, intervals):
            e = ret = 0
            start = sorted(i[0] for i in intervals)
            end = sorted(i[1] for i in intervals)
            
            for s in range(len(start)):
                  if start[s] < end[e]: 
                  ret += 1
                  else: 
                  e += 1
            return ret


      11. two pointer - 大小（前后指针）(对比指针，小的移动)，
      34. 有序数组找数：binary search O(log(n)) 
      75. sort colors （三色问题）: one pass, 前后两指针
      118. 帕斯卡三角: 内外双loop num[i] = prev[i-1] + prev[i];



# Database
      * Gap and island 问题， 通过多次分组排序，确定同源组 DB1454
      * 连续问题： cross join 或者 lag lead
      * 阶梯理论 （hierarchy）:
            使用recursive cte， 确定好每次的继承关系和初始例

      * 

# Git命令
      cd到指定目录
      * 全局指令如: git config --global user.name "xxx" | user.email "xxx@xxx.com"
      
      * mkdir, touch分别为创建文件夹及文件；rm -r, rm为对应删除操作
      * 检查ssh key: ~/.ssh; 生成ssh key: ssh-keygen -t rsa -C "xxx@xxx.com"
      * 检查历史commit记录：git log 
      
      * 建立远程连接（添加远程仓库，用ssh连接）：1.git init 2.git remote add origin git@github.com:xxx.git
      * 检查本地仓库连接：git remote -v
            * 下拉代码：(如果是有权限的仓库) git pull origin master (origin为自己给远程仓库的命名，master为远程仓库分支名) 
                  (如果是无权限的仓库) (非更新) git clone xxx.git
                  
               **另：git pull = git merge + git merge （拉数据，不修改本地commit和文件 + 改变本地数据）
                  
            * 上传代码：1.git add -A 提交所有变化, git add . 提交新文件和被修改文件，不包括删除文件， git add xxx/*.xxx
                       2.git commit -m "xxx" 暂存区文件保存到仓库历史记录，添加注释
                       3.git push -u 本地仓库名 分支 (git push -u origin master)
            
