# Array: 
      
      避免duplicate，可以使用set作为结果容器，会自动消除duplicate
      Hash table - switch key and value pair
      two pointer - 大小（前后指针）
      
      找最大减：max, min更新， greedy method
      找缺失值：用set(...) in; 求和; XOR
      找最大subarray: Greedy, DP
      sort colors: 三指针，前后中
      三数sum：1. sort整个数列，设当前i，对剩余数组进行双指针找sum <- 简化成二数sum问题, 
                 TC: O(n**2) -> 找两数sum O(n) for n times, 存储array O(nlogn) -> O(nlogn + n**2)
                 SC: O(n) -> O(logn) ~ O(n)
              2. hash table, 同1方法，sort整个数列，设立当前i，然后对剩余的数组建立dictionary来找到target,
                 TC: O(n**2) -> 建立hash table O(n) for n times, 存储array O(nlogn) -> O(nlogn + n**2)
                 SC: O(n) for the hashset
                 *如果不sort数列也可以，但为了确保没有duplicate需要对结果进行tuple(sorted((a,b,c))处理
      118. 帕斯卡三角: 内外双loop num[i] = prev[i-1] + prev[i];



# Database
      * Gap and island 问题， 通过多次分组排序，确定同源组 DB1454
      * 连续问题： cross join 或者 lag lead
      * 阶梯理论 （hierarchy）:
            使用recursive cte， 确定好每次的继承关系和初始例

