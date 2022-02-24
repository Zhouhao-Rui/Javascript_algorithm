# Javascript_algorithm
beginner for ALGORITHM, and this is a recording of LeetcodeCN problems with javascript :)


## --二分归并

33. 旋转数组

整数数组 nums 按升序排列，数组中的值 互不相同 。

在传递给函数之前，nums 在预先未知的某个下标 k（0 <= k < nums.length）上进行了 旋转，使数组变为 [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]（下标 从 0 开始 计数）。例如， [0,1,2,4,5,6,7] 在下标 3 处经旋转后可能变为 [4,5,6,7,0,1,2] 。
    
给你 旋转后 的数组 nums 和一个整数 target ，如果 nums 中存在这个目标值 target ，则返回它的下标，否则返回 -1 。
    
**example**
    
    ```javascript
    输入：nums = [4,5,6,7,0,1,2], target = 0
    输出：4
    ```

思路：找到最小或者最大值下标，之后就是两个区间用二分查找

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function(nums, target) {
    // 找到最小的值
    let min = 10
    for (let i = 0; i < nums.length; i ++) {
        if (nums[i] < min) {
            min = nums[i];
        }
    }
    // 二分查找，比较target和left，right
    if (target >= nums[0]) {
        let left = 0
        let right = nums.indexOf(min) - 1    
        while (left <= right) {
            let middle = Math.floor((left + right) / 2)
            if (nums[middle] < target) {
                left = middle + 1
            }
            if (nums[middle] > target) {
                right = middle - 1
            }
            if (nums[middle] == target) {
                return middle
            }
        }
    }

    if (target <= nums[nums.length - 1]) {
        let left = nums.indexOf(min)
        let right = nums.length - 1
        while (left <= right) {
            let middle = Math.floor((left + right) / 2)
            if (nums[middle] < target) {
                left = middle + 1
            }
            if (nums[middle] > target) {
                right = middle - 1
            }
            if (nums[middle] == target) {
                return middle
            }
        }
    }
    return -1
};  
```

69. X的平方根

给你一个非负整数 x ，计算并返回 x 的 算术平方根 。

由于返回类型是整数，结果只保留 整数部分 ，小数部分将被 舍去 。

注意：不允许使用任何内置指数函数和算符，例如 pow(x, 0.5) 或者 x ** 0.5 。

思路：直接二分，但是middle的取值是value，不是index，需要进行一些转换

```javascript
/**
 * @param {number} x
 * @return {number}
 */
var mySqrt = function (x) {
    let left = 0
    let right = x
    while (left <= right) {
        let mid = Math.floor(left + (right - left)/2)
        if (mid * mid < x) {
            left = mid + 1
        } else if (mid * mid > x) {
            right = mid - 1
        } else {
            return mid
        }
    }
    return right
};
```


