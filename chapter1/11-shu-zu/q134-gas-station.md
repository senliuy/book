# 134. Gas Station

直达：https://leetcode.com/problems/gas-station/description/

There areNgas stations along a circular route, where the amount of gas at stationiis`gas[i]`.

You have a car with an unlimited gas tank and it costs`cost[i]`of gas to travel from stationito its next station \(i+1\). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

**Note:**  
The solution is guaranteed to be unique.

## 分析

难点是理清思路，分析出该问题存在的几个性质。

1. 如果gas\[i\] &lt; cost\[i\]，则i不能作为起点；
2. 对所有路径求和，如果$$\sum{(gas[i] - cost[i])} > 0$$，则一定存在一点可以遍历整个环。

问题是当确定能够便利之后，如何确定起点：

性质1：如果i能够作为起点，则从i出发可以到任何一个点；

性质2：如果i是唯一的一个点，选择不存在点j可以到i；

性质3：如果i是唯一的一个点，则i一定可以到i+1到n，0到i-1一定不能到i

根据上面三个性质，得到解决问题的思路





