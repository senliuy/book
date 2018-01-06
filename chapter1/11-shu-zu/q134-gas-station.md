# 134. Gas Station

直达：[https://leetcode.com/problems/gas-station/description/](https://leetcode.com/problems/gas-station/description/)

There areNgas stations along a circular route, where the amount of gas at stationiis`gas[i]`.

You have a car with an unlimited gas tank and it costs`cost[i]`of gas to travel from stationito its next station \(i+1\). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

**Note:**  
The solution is guaranteed to be unique.

## 分析

难点是理清思路，分析出该问题存在的几个性质。

性质1：如果gas\[i\] &lt; cost\[i\]，则i不能作为起点；

性质2：对所有路径求和，如果$$\sum{(gas[i] - cost[i])} > 0$$，则一定存在一点可以遍历整个环。

问题是当确定能够便利之后，如何确定起点：

性质3：如果i能够作为起点，则从i出发可以到任何一个点；

性质4：如果i是唯一的一个点，选择不存在点j可以到i；

性质5：如果i是唯一的一个点，则i一定可以到i+1到n，0到i-1一定不能到i

根据上面三个性质，得到解决问题的思路：

1. 根据性质2，遍历两个数组，确定能不能完成环的遍历；能的话，进入2，否则直接返回-1；
2. 根据性质5，从0出发，查找0不能到的i，如果i+1能到n，则可以返回i+1, 如果i+1不能到n，则将i更新为i能到的最近的节点。

## C++代码

```cpp
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int sum = 0;
        int cur_start = 0;
        int res = 0;
        for (int i=0; i<gas.size(); i++){
            sum += (gas[i] - cost[i]);
            cur_start += (gas[i] - cost[i]);
            if (cur_start < 0){
                cur_start = 0; //重新开始计数
                res = i+1;
            }
        }
        if (sum < 0) return -1;
        else{
            if(res >= gas.size()) return 0;
            else return res;
        }
    }
};
```



