- [排序算法](#排序算法)
  - [1. 冒泡排序（Bubble Sort）](#1-冒泡排序bubble-sort)
    - [时间复杂度：`O(n^2)`](#时间复杂度on2)
    - [步骤](#步骤)
    - [实现](#实现)
  - [2. 选择排序（Selection Sort）](#2-选择排序selection-sort)
    - [时间复杂度：`O(n^2)`](#时间复杂度on2-1)
    - [步骤](#步骤-1)
    - [实现](#实现-1)
  - [3. 插入排序（Insertion Sort）](#3-插入排序insertion-sort)
    - [时间复杂度：`O(n^2)`](#时间复杂度on2-2)
    - [步骤](#步骤-2)
    - [实现](#实现-2)
  - [4. 快速排序（Quick Sort）](#4-快速排序quick-sort)
    - [时间复杂度：`O(nlogn)`](#时间复杂度onlogn)
    - [步骤](#步骤-3)
    - [实现](#实现-3)
  - [5. 希尔排序（Shell Sort）](#5-希尔排序shell-sort)
    - [时间复杂度：`O(nlogn)`](#时间复杂度onlogn)
    - [步骤](#步骤-4)
    - [实现](#实现-4)
  - [6. 归并排序（Merge Sort）](#6-归并排序merge-sort)
    - [时间复杂度：`O(nlogn)`](#时间复杂度onlogn)
    - [步骤](#步骤-5)
    - [实现](#实现-5)
  - [7. 堆排序（Heap Sort）](#7-堆排序heap-sort)
    - [时间复杂度：`O(nlogn)`](#时间复杂度onlogn)
    - [步骤](#步骤-6)
    - [实现](#实现-6)
  - [8. 计数排序（Counting Sort）](#8-计数排序counting-sort)
    - [时间复杂度：`O(n + k)`](#时间复杂度on--k)
    - [步骤](#步骤-7)
    - [实现](#实现-7)
  - [9. 桶排序（Bucket Sort）](#9-桶排序bucket-sort)
    - [时间复杂度：`O(n + k)`](#时间复杂度on--k)
    - [步骤](#步骤-8)
    - [实现](#实现-8)
  - [10. 基数排序（Radix Sort）](#10-基数排序radix-sort)
    - [时间复杂度：`O(nk)`](#时间复杂度onk)
    - [步骤](#步骤-9)
    - [实现](#实现-9)
  - [排序算法总结](#排序算法总结)
    - [常用语言底层排序的使用](#常用语言底层排序的使用)

# 排序算法

十大排序算法：冒泡排序、选择排序、插入排序、快速排序、希尔排序、归并排序、堆排序、计数排序、桶排序、基数排序

## 1. 冒泡排序（Bubble Sort）

类似元素经由交换慢慢“浮”到数列的顶端

### 时间复杂度：`O(n^2)`

### 步骤

1. 比较相邻的元素
    - 如果第一个比第二个大，则交换
2. 对每一对相邻的元素作同样的工作
    - 从第一对到结尾最后一对，这样最后的元素应该是最大的
3. 针对所有元素进行以上步骤，除了最后一个
4. 重复步骤1～3，直到排序完成

### 实现

```javascript {.line-numbers}
function bubbleSort(nums) {
  if (nums.length === 0) return nums
  // 循环 数组长度 的次数
  for (let i = 0, len = nums.length; i < len; i++) {
    // 从 0个 元素，依次和后面元素比较
    // 不需要循环到末尾： 第 [len - 1 - i] 个元素已经冒泡到合适的位置，无需进行比较，减少比较次数
    for (let j = 0; j < len - 1 - i; j++) {
      if (nums[j] > nums[j + 1]) {
        //元素交换
        let temp = nums[j + 1]
        nums[j + 1] = nums[j]
        nums[j] = temp
      }
    }
  }
  return nums
}
```

## 2. 选择排序（Selection Sort）

与冒泡排序类似，可以看成是优化

- 冒泡：相邻元素
- 选择：整体中选择

> 确定最大最小后交换，减少了交换次数

### 时间复杂度：`O(n^2)`

### 步骤

1. 首先，找到最小（大）的元素
2. 其次，将它和数组的第一个元素交换位置
3. 再次，在剩下的元素中找到最小（大）的元素，将它与数组第二个元素交换位置
4. 重复直到将整个数组排序

### 实现

```javascript {.line-numbers}
function choiceSort(nums) {
  if (nums.length === 0) return nums
  for (let i = 0, len = nums.length; i < len; i++) {
    // 最小数下标
    // 每次循环开始假设第一个数最小
    let minIndex = i
    for (let j = i; j < len; j++) {
      // 找到最小值
      if (nums[j] < nums[minIndex]) {
        // 保存最小值下标
        minIndex = j
      }
    }
    // 第i个元素 与 最小数 交换
    let temp = nums[minIndex]
    nums[minIndex] = nums[i]
    nums[i] = temp
  }
  return nums
}
```

## 3. 插入排序（Insertion Sort）

非交换位置，而是找到相应位置并插入

### 时间复杂度：`O(n^2)`

对一个很大且其中的元素已经有序（或接近有序）的数组进行排序将会比对随机顺序的数组或是逆序数组进行排序要快得多

> 对于比分有序的数组十分高效，也适合小规模数组

### 步骤

1. 对于未排序的数据，在已排序序列中从后向前扫描，找到相应的位置插入
2. 为了给插入的元素腾出空间，将插入位置之后的已排序元素都向右移动一位

### 实现

```javascript {.line-numbers}
function insertionSort(nums) {
  if (nums.length === 0) return nums
  // 当前待排序数据
  // 该元素之前的元素均已排序
  let currentValue
  for (let i = 0, l = nums.length - 1; i < l; i++) {
    // 已排序数据的下标
    let preIndex = i
    // 待排序数据
    // 待排序下标 preIndex + 1
    currentValue = nums[preIndex + 1]
    // 在已排序数据中 倒序 寻找合适的插入位置
    // 待排序 < 比较元素
    // 比较元素向后移动一位
    while (preIndex >= 0 && currentValue < nums[preIndex]) {
      // 比较元素后移一位
      nums[preIndex + 1] = nums[preIndex]
      preIndex--
    }
    // while 循环结束，找到合适的位置插入
    nums[preIndex + 1] = currentValue
  }
  return nums
}
```

> 若从 1 开始（理解为首个元素默认是有序的，因此可从 1 开始）：
>
> - l = nums.length
> - preIndex = i - 1
> - currentValue = nums[i]

## 4. 快速排序（Quick Sort）

对冒泡排序的一种改进，也是采用分治法的一个典型的应用

### 时间复杂度：`O(nlogn)`

### 步骤

1. 任意选取一个数据（比如第一个）作为关键数据，称为基准数据
2. 然后将所有比它小的数放它前面，比它大的放后面，这个过程称为一趟 __快速排序__，也称为 __分区（partition）操作__
3. 通过一趟快速排序将要排序的数据分割成独立的两部分，其中一部分所有数据都比另一部分小，再分别进行快速排序，递归进行，达到整个数据变成有序序列

### 实现

不借助额外空间

1. 初始化
    - 选取基准数据
    - 基准数据与末尾数据交换
    - 分区指示器指向第一个元素下标 - 1
2. 遍历
    - 当前元素 <= 基准数据，分区指示器右移一位
    - 当前元素下标 > 分区指示器的下标，分区指示器指向的元素与当前元素交换

```javascript {.line-numbers}
function quickSort(nums) {
  return sort(nums, 0, nums.length - 1)
}

function sort(array, start, end) {
  if (array.length < 1 || start < 0 || end >= array.length || start > end) return null
  // 数据分割成独立的两部分
  // 分区指示器
  let zoneIndex = partition(array, start, end)
  if (zoneIndex > start) {
    sort(array, start, zoneIndex - 1)
  }
  if (zoneIndex < end) {
    sort(array, zoneIndex + 1, end)
  }
  return array
}

// 快速排序分区方法
function partition(array, start, end) {
  // 只有一个元素时不需分区
  if (start === end) return start
  // 随机选取一个基准数
  let pivot = Math.floor(Math.random() * (end - start) + start)
  // 分区指示器，初试值为分区首元素下标 - 1
  let zoneIndex = start - 1
  console.log('开始下标:' + start + ',结束下标:' + end + ',基准数下标:' + pivot + ',元素值' + array[pivot] + ',分区指示器:' + zoneIndex)
  // 将基准数与分区尾元素交换位置
  swap(array, pivot, end)
  for (let i = start; i <= end; i++) {
    // 当前元素 <= 基准元素
    if (array[i] <= array[end]) {
      // 分区指示器累加
      zoneIndex++
      // 当前元素下标 > 分区指示器下标，交换
      if (i > zoneIndex) {
        swap(array, i, zoneIndex)
      }
    }
  }
  return zoneIndex
}

// 交换数组内两个元素
function swap(array, i, j) {
  let temp = array[i]
  array[i] = array[j]
  array[j] = temp
}
```

## 5. 希尔排序（Shell Sort）

简单插入排序的改进版；它与插入排序的不同之处在于，它会优先比较距离较远的元素。希尔排序又叫 __缩小增量排序__

### 时间复杂度 `nlogn`

### 步骤

1. 按一定增量分组，对每组使用插入排序算法排序
2. 然后缩小增量继续分组排序，直到增量减至1

> 这个不断减小的增量，就构成了一个增量序列

#### 案例

例如：[x, x, x, x, x, x, x, x]

```
gap = length / 2
gap = gap / 2
// 增量序列{4, 2, 1}
```

第一个增量为4，则原始数据分为4组，组内每个元素之间下标之差为4，这4组分别进行插入排序
第二个增量...

> 增量序列是递减，且最后为1 则都可以使用
> 目前还无法证明某个序列是“最好的”

#### 常用增量序列

- 希尔增量序列：`{N/2, (N/2)/2, ..., 1}`
- Hibbard 序列：`{2^k-1, ..., 3, 1}`
- Sedgewick 序列：`{..., 109, 41, 19, 5, 1}` 表达式：$9 * 4^i - 9 * 2^i + 1$ 或者 $4^i - 3 * 2^i + 1$

### 实现

```javascript {.line-numbers}
function shellSort(nums) {
  let len = nums.length
  // 按增量排序排序后，每个分组中
  // temp 代表当前待排序数据
  // 该元素之前的组内元素均已被排序过
  let currentValue
  // 相较插入排序：表示分组的增量，依次递减
  let gap = Math.floor(len / 2)
  while (gap > 0) {
    // 组内排序
    for (i = gap; i < len; i++) {
      currentValue = nums[i]
      // 组内已被排序数据的索引
      let preIndex = i - gap
      // 已被排序过的数据中倒序找合适的位置
      // 当前排序数据 < 比较的元素，比较的元素后移一位
      while (preIndex >= 0 && nums[preIndex] > currentValue) {
        nums[preIndex + gap] = nums[preIndex]
        preIndex -= gap
      }
      // while 循环结束
      // 说明已经找到了当前待排序数据合适位置，插入
      nums[preIndex + gap] = currentValue
    }
    console.log('本轮增量：【', gap, '】排序后的数组')
    console.log(nums)
    console.log('--------------------')
    gap = Math.floor(gap / 2)
  }
  return nums
}
```

## 6. 归并排序（Merge Sort）

对于给定的一组数据，利用 递归 和 分治技术将数据序列划分成为越来越小的半子表，在对半子表排序后，再用递归方法将排序好的半子表合并成为越来越大的有序序列

### 时间复杂度：`O(nlogn)`

### 步骤

1. 拆分，直到每个孙子表剩2个元素
2. 每个孙子表排序，得到有序孙子表
3. 准备空白数组，孙子表两两比较，分别拿出一个比较，依次放入
4. 获得的子表继续两两比较

### 实现

```javascript {.line-numbers}
function mergeSort(nums) {
  if (nums.length < 2) return nums
  // 拆分数组，然后递归排序，并用 merge 合并
  let mid = Math.floor(nums.length / 2)
  let left = nums.slice(0, mid)
  let right = nums.slice(mid, nums.length)
  return merge(mergeSort(left), mergeSort(right))
}

// 将两段排序好的数组结合成一个排序数组
function merge(left, right) {
  let result = Array.from({ length: left.length + right.length })
  for (let index = 0, i = 0, j = 0, len = result.length; index < len; index++) {
    // - 考虑一边已经取完，另一边直接赋值
    // - 否则比较
    if (i >= left.length) {
      // 左边数组已经取完，取右边数组的值即可
      result[index] = right[j++]
    } else if (j >= right.length) {
      // 右边数组已经取完，取左边数组的值即可
      result[index] = left[i++]
    } else if (left[i] > right[j]) {
      // 左边数组的元素 > 右边数组元素，取右边
      result[index] = right[j++]
    } else {
      // 右边数组的元素 > 左边数组元素，取左边
      result[index] = left[i++]
    }
  }
  console.log('左子数组：', left)
  console.log('右子数组：', right) 
  console.log('合并后：', result)
  return result
}
```

> 1. 划分几份并没有什么约束，例如：一分为二等
> 2. 有时考虑到性能，当分组到一定大小后采用插入排序、希尔排序对子数组排序

## 7. 堆排序（Heap Sort）

利用堆这种数据结构所设计的一种排序算法

> 堆积是一个近似完全二叉树的结构，并同时满足堆积的性质：即子结点的键值或索引总是小于（或者大于）它的父结点

### 时间复杂度：`O(nlogn)`

### 步骤

1. 将数组视为一个完全二叉树
2. 找到最后一个非叶子结点（`length / 2 - 1`，[完全二叉树推论](Tree.md?plain=1#L90)），和其叶子结点们比较（需要则交换）
3. 从2可得，小于其下标的都是非叶子结点
4. 倒序遍历非叶子结点，与它们的叶子结点们比较（需要则交换）
5. 当根结点（首元素）与其子结点交换后
    - 可能导致其子树再次不满足堆定义（原根结点比较小，比子树的子结点更小）
6. 交换后的 __原根节__ 点继续和其子结点比较（需要则交换）,最后得到 __二叉堆__
    - 最大堆 → 升序数组
    - 最小堆 → 降序数组
7. __开始堆排序__：将堆顶元素和尾元素交换
8. 并将交换后的 __尾元素__ 不再视为二叉树的一部分（脱离）
9. 继续检视二叉树，调整使其重新满足二叉堆（进行 5~6）
10. 二叉堆继续排序（进行 7~9）直到排序完成

### 实现

```javascript {.line-numbers}
function heapSort(nums) {
  let len = nums.length
  if (len < 1) return nums
  // 构建最大堆
  buildMaxHeap(nums)
  // 见步骤 7，循环:
  // 将堆首（最大值）与未排序数据末尾交换
  // 然后重新调整为最大堆
  while (len > 0) {
    swap(nums, 0, len - 1)
    // 见步骤 8
    len--
    // 见步骤 9
    // 继续调整，使其满足二叉堆
    adjustHeap(nums, 0, len)
    console.log(nums)
    console.log('----------')
  }
  return nums
}

// 交换数组内两个元素
function swap(array, i, j) {
  let temp = array[i]
  array[i] = array[j]
  array[j] = temp
}

// 建立最大堆（与 使之成为最大堆 逻辑一样）
function buildMaxHeap(array) {
  const len = array.length
  // (一定是)从最后一个非叶子结点开始向上构造最大堆
  // 见步骤 3
  let i = Math.floor(len / 2) - 1
  for (; i >= 0; i--) {
    adjustHeap(array, i, len)
  }
  console.log('构造最大堆', array)
  console.log('====================')
}

// 调整使之成为最大堆
function adjustHeap(array, i, len) {
  let maxIndex = i
  // 完全二叉树推论
  let left = 2 * i + 1
  let right = 2 * (i + 1)
  // 见步骤 4
  // 如果有左子树，且 左子树 > 父结点
  // 则将最大指针指向左子树
  if (left < len && array[left] > array[maxIndex]) {
    maxIndex = left
  }
  // 如果有右子树，且 右子树 > 父结点
  // 则将最大指针指向右子树
  if (right < len && array[right] > array[maxIndex]) {
    maxIndex = right
  }
  // 见步骤 5
  // 如果父结点不是最大值，则将父结点与最大值交换
  if (maxIndex !== i) {
    swap(array, maxIndex, i)
    // 见步骤 6
    // 会影响到已调整过的，故递归调整与父结点交换的位置
    // 父结点已经是最大值 maxIndex
    adjustHeap(array, maxIndex, len)
  }
}
```

## 8. 计数排序（Counting Sort）

核心在于将输入的数据值转化为键存储在额外开辟的数组空间中。

作为一种线性时间复杂度的排序，计数排序要求输入的数据必须是有 __确定范围的整数__ 。

> 计数排序、基数排序、桶排序都利用了桶的概念，对桶的使用方法有差异

### 时间复杂度：`O(n + k)`

### 步骤

如果一个数组里所有元素都是整数，而且在 `0~k` 之间
如果能知道数组里有多少项小于或等于该元素，就能准确给出该元素在排序后数组的位置

1. 初始化一个计数数组
2. 遍历原始数组，并修改计数数组的值（元素值转化为下标，+1）
3. 遍历计数数组，修改原始数组为当前下标值（计数数组元素值 -1）
    - 计数数组元素值 != 0，移动原始数组索引，继续修改并-1
    - 计数数组元素值 == 0，移动计数数组索引

#### 案例

`[2, 5, 3, 0, 2, 3, 0, 3]`

对于数组，元素5之前有8个元素小于等于5（含5本身），因此排序后5肯定是在位置7，只要构造一个（5 + 1）大小的数组，里面存下所有对应每个元素之前的元素个数，就能在线性时间内完成排序

#### 计数数组长度

- `[1003, 1001, 1030, 1050]` 并不需要建立 `1050 + 1` 的数组
计数数组确认：`1050 - 1003 + 1 = 48`

- `[99999, 1, 2]` 依照上例，需要 `99999 - 1 + 1` 的空间，实在浪费

> 所以计数排序适用于连续、跨度小的的情况

### 实现

```javascript {.line-numbers}
function countingSort(nums) {
  const len = nums.length
  if (!len) return nums
  let bias
  let min = nums[0]
  let max = nums[0]
  // 获取待排序数组的最大、最小值
  for (let i = 0; i < len; i++) {
    if (nums[i] > max) max = nums[i]
    if (nums[i] < min) min = nums[i]
  }
  // 偏移量，用以定位原始数组每个元素在计数数组中的下标
  bias = 0 - min
  // 获得计数数组大小
  let count = Array.from({ length: max - min + 1 }, () => 0)

  // 遍历原始数组
  // 将每个元素转化为计数数组下标，并按个数累加
  for (let i = 0; i < len; i++) {
    count[nums[i] + bias]++
  }

  // 原始数组下标计数器
  let index = 0
  // 计数数组下标计数器
  let i = 0
  while (index < len) {
    if (count[i]) {
      nums[index] = i - bias
      count[i]--
      index++
    } else {
      i++
    }
    console.log(count)
    console.log(nums)
    console.log('----------')
  }
  return nums
}
```

## 9. 桶排序（Bucket Sort）

计数排序的升级版

假设输入数据服从均匀分布，将数据分到有限数量的桶里，每个桶再分别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排

### 时间复杂度：`O(n + k)`

### 步骤

1. 建立桶
2. 将元素按区间放入桶中
3. 各个桶分别进行排序（插入、快速等）
4. 依次取出桶中的元素

#### 案例

`[35, 23, 48, 9, 16, 24, 5, 11, 32, 17]`

建立5个桶：[0, 10)、[10, 20)、[20, 30)、[30, 40)、[40, 50) 左闭右开区间，放入5个桶分别排序，依次取出5个桶中的元素，得到排序后的序列

### 实现

桶排序中保证元素均匀分布到各个桶尤为关键（极端的例子：所有待排序元素都落在同一个桶中）

为了保证均匀分布，我们限定桶的容量，再根据元素个数来决定桶的个数

```javascript {.line-numbers}
function bucketSort(nums, bucketCap) {
  if (!Array.isArray(nums) || nums.length < 2) return nums
  const len = nums.length
  let max = nums[0]
  let min = nums[0]
  // 找到最大、最小值
  for (let i = 0; i < len; i++) {
    if (nums[i] > max) max = nums[i]
    if (nums[i] < min) min = nums[i]
  }

  // 获取桶数量
  let bucketCount = Math.floor((max - min) / bucketCap) + 1
  // 桶数组
  let bucketArr = []
  let resultArr = []
  // 构建桶
  for (let i = 0; i < bucketCount; i++) {
    bucketArr.push([])
  }
  // 将数据分配到桶中
  for (let i = 0; i < len; i++) {
    const item = nums[i]
    const index = Math.floor((item - min) / bucketCap)
    bucketArr[index].push(item)
  }

  // 看看桶中数据的分布
  for (let i = 0; i < bucketCount; i++) {
    console.log('第', i, '个桶包含数据：')
    console.log(bucketArr[i])
  }

  // 桶内数据排序
  for (let i = 0; i < bucketCount; i++) {
    // 每个桶里只有1个元素，依次取出
    if (bucketCap === 1) {
      for (let j = 0, jLen = bucketArr[i].length; j < jLen; j++)
      resultArr.push(bucketArr[i][j])
    } else {
      // 当只能划分一个桶时，减少每个桶元素的上限
      // 增加桶的数量（缩小每个桶的区间）
      if (bucketCount === 1) {
        bucketCap--
      }
      console.log('对第', i, '桶中的数据再次用桶进行排序', '每个桶最多放', bucketCap, '个元素')
      // 递归使用桶排序
      const temp = bucketSort(bucketArr[i], bucketCap)
      // 依次取出
      for (let j = 0, jLen = temp.length; j < jLen; j++) {
        resultArr.push(temp[j])
      }
    }
  }
  return resultArr
}
```

## 10. 基数排序（Radix Sort）

非比较的排序算法。数据元素由若干位组成（字符串、整数）

### 时间复杂度：`O(nk)`

### 步骤

1. 从右往左依次将每一位当做一次关键字对数组元素入桶
2. 每一轮入桶都基于上轮入桶结果，完成所有位入桶，达到有序

#### 案例

`[35, 23, 48, 9, 16, 24, 5, 11, 32, 17, 70, 56]`

个位入桶：

```
0：70
1: 11
2: 32
...
9: 9
```
得到：`[70, 11, 32, 23, 24, 35, 5, 56, 16, 17, 48, 9]`

十位入桶：

```
0: 5, 9
1: 11, 16, 17
...
7: 70
8:
9:
```
最终得到：`[5, 9, 11, 16, 17, 23, 24, 32, 35, 48, 56, 70]`

#### 桶相关排序的比较

基数排序、计数排序和桶排序都利用了桶的概念，但对桶的使用有差异：

- 基数排序：根据键值的每位数字来分配桶
- 计数排序：每个桶只存储单一键值
- 桶排序：每个桶存储一定范围的数值

### 实现

十进制整数：每一位10种可能，10就是基

二进制数字：基为2

字符串（8位的扩展ASCII）：基是256

...

```javascript {.line-numbers}
function radixSort(nums) {
  if (!Array.isArray(nums) || nums.length < 2) return nums
  const len = nums.length
  // 找出最大数
  let max = nums[0]
  for (let i = 0; i < len; i++) {
    max = Math.max(nums[i], max)
  }

  // 算出最大位数，用来确定进行几轮排序
  let maxDigit = 0
  while (max != 0) {
    max = parseInt(max / 10)
    maxDigit++
  }

  // 构建桶
  // bucketCount = 10
  // 每一位都是 0~9 10个数字，所以分10个桶
  const bucketCount = 10
  let bucketList = Array.from({ length: bucketCount }, () => [])
  
  let mod = 10
  let div = 1
  // 从右往左，每一位作为关键字排序，每一轮基于上一轮的结果排序
  for (let i = 0; i < maxDigit; i++, mod *= 10, div *= 10) {
    // 遍历原始数组，投入到各个桶
    for (let j = 0; j < len; j++) {
      const item = nums[j]
      const index = Math.floor((item % mod) / div)
      bucketList[index].push(item)
    }

    // 输出桶中分布
    for (let b = 0, bLen = bucketList.length; b < bLen; b++) {
      console.log('第', b, '个桶包含：', bucketList[b])
    }

    // 桶中的数据写回原始数组
    nums = bucketList.reduce((previousValue, currentValue) => {
      return previousValue.concat(currentValue)
    }, [])
    // 清除桶，准备下一轮排序
    bucketList = Array.from({ length: bucketCount }, () => [])
  }
  return nums
}
```

## 排序算法总结

&nbsp; | 平均时间复杂度 | 最好情况 | 最坏情况 | 空间复杂度 | 稳定性 | 比较算法
------------ | - | - | - | - | - | -------------
冒泡排序 | `O(n^2)` | `O(n)` | `O(n^2)` | `O(1)` | 稳定 | 是
选择排序 | `O(n^2)` | `O(n^2)` | `O(n^2)` | `O(1)` | 不稳定 | 是
插入排序 | `O(n^2)` | `O(n)` | `O(n^2)` | `O(1)` | 稳定 | 是
希尔排序 | `O(nlogn)~O(n^2)` | `O(n^1.3)` | `O(n^2)` | `O(1)` | 不稳定 | 是
归并排序 | `O(nlogn)` | `O(nlogn)` | `O(nlogn)` | `O(n)` | 稳定 | 是
快速排序 | `O(nlogn)` | `O(nlogn)` | `O(n^2)` | `O(logn)` | 不稳定 | 是
堆排序 | `O(nlogn)` | `O(nlogn)` | `O(nlogn)` | `O(1)` | 不稳定 | 是
计数排序 | `O(n + k)` | `O(n + k)` | `O(n + k)` | `O(k)` | 稳定 | 否
桶排序 | `O(n + k)` | `O(n)` | `O(n^2)` | `O(n + k)` | 稳定 | 否
基数排序 | `O(nk)` | `O(nk)` | `O(nk)` | `O(n + k)` | 稳定 | 否

> __稳定性__：待排序数组中存在 a, b 元素且相等，在排序后顺序保持则称之为 __稳定__；反之若排序后变成 b, a 则为 __不稳定__


### 常用语言底层排序的使用

#### 为什么使用快速排序

实际工作中，各种语言实现排序时都使用了 __快速排序__，为什么不是 __归并排序__ 、__堆排序__ 呢？

从时间复杂度上发现三者几乎一样，但注意一般这里说的 __时间复杂度__ 完整的名称叫 __渐进时间复杂度__（并不是真正的执行时间，而是代码执行时间随着数据规模增长的趋势），实际 __时间复杂度__ 计算时往往隐含 __常数因子__。

- 与 __归并排序__ 比较
    1. __快速排序__ 的常数因子远远小于 __归并排序__
    2. 空间复杂度更小
- 与 __堆排序__ 比较
    1. __堆排序__ 每次拿走根结点后要 _堆重建_，需要消耗时间
- 避免 __快速排序__ 出现最坏情况：优化 _基准数据_ 的选择

#### 为什么使用插入排序

__快速排序__ 针对小到一定规模数据，选择 _基准数据_ 划分会出现不准确的情况导致反复调用，最终出现反复的出栈入栈（__快速排序__ 通过递归实现）。虽然依然保持线性对数阶的时间复杂度，但是可能会超过平方阶的时间。故数据规模小于一定时建议使用 __插入排序__。