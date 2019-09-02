# 题目
TwoSum

## code
```
impl Solution {
    pub fn two_sum(nums: Vec<i32>, target: i32) -> Vec<i32> {
        let mut hMap: std::collections::HashMap<i32, i32> = std::collections::HashMap::new();
        for i in 0..nums.len() {
            let n = nums[i as usize];
            let n2 = target -n;
            if let Some(&pos) = hMap.get(&n2) {
                return vec![pos as i32, i as i32];
            }
            hMap.insert(n, i as i32);
        }
        return vec![];
    }
}
#[cfg(test)]
mod tests {
  use super::*;

#[test]
  fn it_works() {
    assert_eq!(Solution::two_sum(vec![1,2,3,4,5,6], 100), vec![]);
    assert_eq!(Solution::two_sum(vec![1,2,3,4,5,6], 3), vec![0, 1]);
    assert_eq!(Solution::two_sum(vec![1,2,3,4,5,6], 10), vec![3, 5]);
  }
}
```

## 运行结果：
Details 
Runtime: 0 ms, faster than 100.00% of Rust online submissions for Two Sum.
Memory Usage: 3 MB, less than 50.00% of Rust online submissions for Two Sum.

## 思路
通过hashmap，存储已经遍历过的数字以及对应下标，对于新的数n, 查找target - n即可。
### 复杂度：
O(n)
### 困难：
主要是rust HashMap的接口不熟悉
### 可能优化的思路：
如果数比较多的话，放在hashmap种可能不是一种良好的思路，考虑先排序，再往中间寻找结果的方式，空间复杂度为O(1), 时间复杂度为O(nlogn)
### 归类：
动态规划
### 类似： 
n-sum/动态规划题型，4-sum, 3-sum, 最大连续子序列等
