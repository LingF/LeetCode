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
