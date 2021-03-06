***数据结构***

**快速排序（QSort,快拍）算法及C语言实**

》Quick Sort在C语言中自带——qsort函数，包含在<stdlib.h>头文件中。

》快拍是在冒泡排序上改进的一种算法。其基本思想是：通过一次排序将整个无序表分成两部分，其中一部非比另一部分包含的数据小，然后沿用此方法分别对两部分进行同样的排序。直到一个小部分不可再分，所以得到的整个序列成为了有序序列。

》快速排序算法的时间复杂度为O(nlogn),是所有时间复杂度相同的算法中性能最好的算法；重复数据过多时会导致其退化为O(n);

》分而治之，

* 取一个枢纽
* 左边的都小于枢纽右边的都大于枢纽

* 数值中只剩下一个或者零个数

i,j的初始值都为零；

一个数组比枢纽小的 left<=j.比枢纽大的，j<=i;

**堆排序**

堆（大根堆）

* 形状特征：完全二叉树——》顺序存储
* 数值特征：对每个子树，根大于右孩子，根大于左孩子；
* 对N个数建堆；
* 把堆顶放到最后（重复上面和此步骤）；

最后一个父亲节点为N/2，依次到递减到1；

兄弟，父子如果交换，向下循环；

》通过将无序表转化为堆，可以直接找到表中的最大值或者最小值，然后将其提取出来，令剩下的记录在重建一个堆，取出次大值或者次小值，如此反复执行，得到一个有序序列，此过程为堆排序；

堆排序需要解决两个问题：

》如何将一个无序序列转化为一个堆

》在输出堆顶元素后，如何调整剩余元素构建一个新堆；

***B树-多叉平衡搜索树***

* 每一个结点最多由m个子节点（m阶，m不小于3）
* 每个内部结点最少有[m/2]-1个，最多有m-1个
* 如果根结点不是叶子结点，那么他至少有两个子节点
* 有k个子节点的非叶子结点拥有k-1个元素
* 所有叶子结点都在同一层
* 其搜索性能等价于在关键字集合内做一次二分查找,因为每个结点的关键字在左右字树中都是有序的，所以只要比较结点中的关键字，或者沿着指针就能很快的找到关键字，如果查找失败，则会返回叶子结点，即空指针。

**B树的插入**

所有的插入都从根节点开始。要插入一个新的元素，首先要搜索这个树找到新元素应该被添加的叶子节点，将新元素插到这一结点，且保持结点中数据有序。

否者的话这个结点已满，将他们平均分裂成两个结点，且保持元素中有序。

* 从叶子结点的元素和新的元素中选出中位数
* 小于这一中位数的元素发到左边结点，大于这一中位数的元素放到右边结点，中位数作为分隔值。
* 分隔值（中位数）上提，插入到父亲结点中，这可能会造成父亲结点分裂，分裂父亲结点时又有可能造成他的父亲结点分裂，以此类推

***B+树***

* 非叶子结点不存储data，只存储key
* 所有的非叶子结点存储完整的一份key信息以及key对应的data，
* 所以每一个父节点出现在子节点中，是子节点最大或者最小元素
* 每个叶子结点都有一个指针，指向下一个结点，形成一个链表

**B+数的查找过程**

与B树类似，只不过查找时，如果在非叶子结点的关键值等于给定值，并不会终止，而是继续沿着直到叶子结点位置。因此在B+树中不管查找成功与否，每次查找都是走了一条从从根到叶子结点的路径。