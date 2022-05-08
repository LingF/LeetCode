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

## 排序算法

十大排序算法：冒泡排序、选择排序、插入排序、归并排序、堆排序、快速排序、希尔排序、计数排序、基数排序、桶排序

### 1. 冒泡排序（Bubble Sort）

类似元素经由交换慢慢“浮”到数列的顶端

#### 时间复杂度：`O(n^2)`

#### 步骤

1. 比较相邻的元素
    - 如果第一个比第二个大，则交换
2. 对每一对相邻的元素作同样的工作
    - 从第一对到结尾最后一对，这样最后的元素应该是最大的
3. 针对所有元素进行以上步骤，除了最后一个
4. 重复步骤1～3，直到排序完成

#### 实现

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

### 2. 选择排序（Selection Sort）

与冒泡排序类似，可以看成是优化

- 冒泡：相邻元素
- 选择：整体中选择

> 确定最大最小后交换，减少了交换次数

#### 时间复杂度：`O(n^2)`

#### 步骤

1. 首先，找到最小（大）的元素
2. 其次，将它和数组的第一个元素交换位置
3. 再次，在剩下的元素中找到最小（大）的元素，将它与数组第二个元素交换位置
4. 重复直到将整个数组排序

#### 实现

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

### 3. 插入排序（Insertion Sort）

非交换位置，而是找到相应位置并插入

#### 时间复杂度：`O(n^2)`

对一个很大且其中的元素已经有序（或接近有序）的数组进行排序将会比对随机顺序的数组或是逆序数组进行排序要快得多

> 对于比分有序的数组十分高效，也适合小规模数组

#### 步骤

1. 对于未排序的数据，在已排序序列中从后向前扫描，找到相应的位置插入
2. 为了给插入的元素腾出空间，将插入位置之后的已排序元素都向右移动一位

#### 实现

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

### 4. 快速排序（Quick Sort）

对冒泡排序的一种改进，也是采用分治法的一个典型的应用

#### 时间复杂度：`O(nlogn)`

#### 步骤

1. 任意选取一个数据（比如第一个）作为关键数据，称为基准数据
2. 然后将所有比它小的数放它前面，比它大的放后面，这个过程称为一趟 __快速排序__，也称为 __分区（partition）操作__
3. 通过一趟快速排序将要排序的数据分割成独立的两部分，其中一部分所有数据都比另一部分小，再分别进行快速排序，递归进行，达到整个数据变成有序序列

#### 实现

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

### 5. 希尔排序（Shell Sort）

简单插入排序的改进版；它与插入排序的不同之处在于，它会优先比较距离较远的元素。希尔排序又叫 __缩小增量排序__

#### 时间复杂度 `nlogn`

#### 步骤

1. 按一定增量分组，对每组使用插入排序算法排序
2. 然后缩小增量继续分组排序，直到增量减至1

> 这个不断减小的增量，就构成了一个增量序列

##### 案例

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

##### 常用增量序列

- 希尔增量序列：`{N/2, (N/2)/2, ..., 1}`
- Hibbard 序列：`{2^k-1, ..., 3, 1}`
- Sedgewick 序列：`{..., 109, 41, 19, 5, 1}` 表达式：$9 * 4^i - 9 * 2^i + 1$ 或者 $4^i - 3 * 2^i + 1$

#### 实现

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