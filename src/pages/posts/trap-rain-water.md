---
title: '接雨水问题解析'
pubDate: 2025-02-20
description: '接雨水问题解析'
author: 'tluuuu'
image:
  url: 'https://docs.astro.build/assets/rose.webp'
  alt: 'The Astro logo on a dark background with a pink glow.'
tags: ['算法', '接雨水']
---

# 接雨水问题详解

发表于：2025-02-20

## 题目描述

给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
返回容器可以储存的最大水量。

## 解题思路

### 1. 双指针法

这是最优的解法，时间复杂度 O(n)，空间复杂度 O(1)。

```typescript
function trap(height: number[]): number {
  if (!height.length) return 0;

  let left: number = 0;
  let right: number = height.length - 1;
  let leftMax: number = 0;
  let rightMax: number = 0;
  let result: number = 0;

  while (left < right) {
    if (height[left] < height[right]) {
      if (height[left] >= leftMax) {
        leftMax = height[left];
      } else {
        result += leftMax - height[left];
      }
      left++;
    } else {
      if (height[right] >= rightMax) {
        rightMax = height[right];
      } else {
        result += rightMax - height[right];
      }
      right--;
    }
  }

  return result;
}
```

### 2. 动态规划法

时间复杂度 O(n)，空间复杂度 O(n)。

```typescript
function trap(height: number[]): number {
  if (!height.length) return 0;

  const n: number = height.length;
  const leftMax: number[] = new Array(n).fill(0);
  const rightMax: number[] = new Array(n).fill(0);

  // 计算左边最大值
  leftMax[0] = height[0];
  for (let i = 1; i < n; i++) {
    leftMax[i] = Math.max(height[i], leftMax[i - 1]);
  }

  // 计算右边最大值
  rightMax[n - 1] = height[n - 1];
  for (let i = n - 2; i >= 0; i--) {
    rightMax[i] = Math.max(height[i], rightMax[i + 1]);
  }

  // 计算结果
  let result: number = 0;
  for (let i = 0; i < n; i++) {
    result += Math.min(leftMax[i], rightMax[i]) - height[i];
  }

  return result;
}
```

## Trae AI

使用了 1 个参考

我来帮你完善这篇关于接雨水问题的博客文章。我会在你现有的内容基础上添加详细的问题描述和解题思路。

````markdown
---
title: '接雨水问题解析'
pubDate: 2025-02-20
description: '接雨水问题解析'
author: 'tluuuu'
image:
  url: 'https://docs.astro.build/assets/rose.webp'
  alt: 'The Astro logo on a dark background with a pink glow.'
tags: ['算法', '接雨水']
---

# 接雨水问题详解

发表于：2025-02-20

## 题目描述

给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

输入：height = [0,1,0,2,1,0,1,3,2,1,2,1]
输出：6
解释：上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水。

## 解题思路

这道题可以用多种方法解决，我们来看几种常见的解法：

### 1. 双指针法

这是最优的解法，时间复杂度 O(n)，空间复杂度 O(1)。

```python
def trap(height):
    if not height:
        return 0

    left, right = 0, len(height) - 1
    left_max = right_max = 0
    result = 0

    while left < right:
        if height[left] < height[right]:
            if height[left] >= left_max:
                left_max = height[left]
            else:
                result += left_max - height[left]
            left += 1
        else:
            if height[right] >= right_max:
                right_max = height[right]
            else:
                result += right_max - height[right]
            right -= 1

    return result
```
````

````

核心思想：

1. 使用双指针 left 和 right 分别从数组两端向中间移动
2. 记录左右两边的最大高度 left_max 和 right_max
3. 如果 height[left] < height[right]，则必定可以接到雨水（取决于 left_max）
4. 如果 height[right] <= height[left]，则必定可以接到雨水（取决于 right_max）
### 2. 动态规划法
时间复杂度 O(n)，空间复杂度 O(n)。

```python
def trap(height):
    if not height:
        return 0

    n = len(height)
    left_max = [0] * n
    right_max = [0] * n

    # 计算左边最大值
    left_max[0] = height[0]
    for i in range(1, n):
        left_max[i] = max(height[i], left_max[i-1])

    # 计算右边最大值
    right_max[n-1] = height[n-1]
    for i in range(n-2, -1, -1):
        right_max[i] = max(height[i], right_max[i+1])

    # 计算结果
    result = 0
    for i in range(n):
        result += min(left_max[i], right_max[i]) - height[i]

    return result
````

核心思想：

1. 对于每个位置，能接的雨水量取决于：min(左边最大高度, 右边最大高度) - 当前高度
2. 提前计算每个位置的左边最大高度和右边最大高度
3. 遍历每个位置计算能接的雨水量

## 复杂度分析

1. 双指针法：

   - 时间复杂度：O(n)，只需要遍历一次数组
   - 空间复杂度：O(1)，只需要常数级别的额外空间

2. 动态规划法：

   - 时间复杂度：O(n)，需要遍历三次数组
   - 空间复杂度：O(n)，需要两个额外的数组存储左右最大值

## 总结

接雨水问题是一个经典的算法题，它的核心在于理解：对于每个位置能接的雨水量，取决于该位置左右两边最大高度的较小值与当前高度的差值。虽然动态规划的思路直观易懂，但双指针法能够将空间复杂度优化到 O(1)，是更优的解法。

```plaintext

这篇文章包含了：
1. 清晰的题目描述和示例
2. 两种主要解法的详细讲解
3. 每种解法的代码实现
4. 算法的核心思想解释
5. 复杂度分析
6. 总结

这样的结构既适合初学者理解，也能帮助读者深入理解算法的本质。
```

## user6148409006254

复制

删除

将其中的 python 代码修改为 typescript

## Trae AI

使用了 1 个参考

我来帮你将解题代码修改为 TypeScript 版本。

````markdown
---
title: '接雨水问题解析'
pubDate: 2025-02-20
description: '接雨水问题解析'
author: 'tluuuu'
image:
  url: 'https://docs.astro.build/assets/rose.webp'
  alt: 'The Astro logo on a dark background with a pink glow.'
tags: ['算法', '接雨水']
---

# 接雨水问题详解

发表于：2025-02-20

## 题目描述

给定一个长度为 n 的整数数组 height 。有 n 条垂线，第 i 条线的两个端点是 (i, 0) 和 (i, height[i]) 。

找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。
返回容器可以储存的最大水量。

## 解题思路

### 1. 双指针法

这是最优的解法，时间复杂度 O(n)，空间复杂度 O(1)。

```typescript
function trap(height: number[]): number {
  if (!height.length) return 0;

  let left: number = 0;
  let right: number = height.length - 1;
  let leftMax: number = 0;
  let rightMax: number = 0;
  let result: number = 0;

  while (left < right) {
    if (height[left] < height[right]) {
      if (height[left] >= leftMax) {
        leftMax = height[left];
      } else {
        result += leftMax - height[left];
      }
      left++;
    } else {
      if (height[right] >= rightMax) {
        rightMax = height[right];
      } else {
        result += rightMax - height[right];
      }
      right--;
    }
  }

  return result;
}
```
````

````

### 2. 动态规划法
时间复杂度 O(n)，空间复杂度 O(n)。

```typescript
function trap(height: number[]): number {
    if (!height.length) return 0;

    const n: number = height.length;
    const leftMax: number[] = new Array(n).fill(0);
    const rightMax: number[] = new Array(n).fill(0);

    // 计算左边最大值
    leftMax[0] = height[0];
    for (let i = 1; i < n; i++) {
        leftMax[i] = Math.max(height[i], leftMax[i-1]);
    }

    // 计算右边最大值
    rightMax[n-1] = height[n-1];
    for (let i = n-2; i >= 0; i--) {
        rightMax[i] = Math.max(height[i], rightMax[i+1]);
    }

    // 计算结果
    let result: number = 0;
    for (let i = 0; i < n; i++) {
        result += Math.min(leftMax[i], rightMax[i]) - height[i];
    }

    return result;
}
````

核心思想：

1. 对于每个位置，能接的雨水量取决于：min(左边最大高度, 右边最大高度) - 当前高度
2. 提前计算每个位置的左边最大高度和右边最大高度
3. 遍历每个位置计算能接的雨水量

## 复杂度分析

1. 双指针法：

   - 时间复杂度：O(n)，只需要遍历一次数组
   - 空间复杂度：O(1)，只需要常数级别的额外空间

2. 动态规划法：

   - 时间复杂度：O(n)，需要遍历三次数组
   - 空间复杂度：O(n)，需要两个额外的数组存储左右最大值

## 总结

接雨水问题是一个经典的算法题，它的核心在于理解：对于每个位置能接的雨水量，取决于该位置左右两边最大高度的较小值与当前高度的差值。虽然动态规划的思路直观易懂，但双指针法能够将空间复杂度优化到 O(1)，是更优的解法。
