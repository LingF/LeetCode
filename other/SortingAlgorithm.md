## 排序算法

十大排序算法：冒泡排序、选择排序、插入排序、归并排序、堆排序、快速排序、希尔排序、计数排序、基数排序、桶排序

### 冒泡排序（Bubble Sort）

类似元素经由交换慢慢“浮”到数列的顶端

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
