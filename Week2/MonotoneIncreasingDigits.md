```rust

impl Solution {
    pub fn monotone_increasing_digits(n: i32) -> i32 {
        const ZERO_ASCII: u8 = 48;
        let str_n = n.to_string();
        let str_n = str_n.as_bytes();
        let mut k: i32 = 0;
        for i in 0..(str_n.len() - 1) {
            if str_n[i] > str_n[i+1] {
                let mut m = i;
                loop {
                    if m == 0 || str_n[m - 1] < str_n[m] {
                        break
                    } else {
                        m -= 1;
                        k /= 10;
                    }
                }
                k *= 10;
                k += ((str_n[m] - 1) - ZERO_ASCII) as i32;
                for _j in (m+1)..str_n.len() {
                    k *= 10;
                    k += 9;
                }
                return k;
            }
            k *= 10;
            k += (str_n[i] - ZERO_ASCII) as i32;
        }
        return n;
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    #[test]
    fn it_works() {
        assert_eq!(Solution::monotone_increasing_digits(1023), 999);
        assert_eq!(Solution::monotone_increasing_digits(7), 7);
        assert_eq!(Solution::monotone_increasing_digits(332), 299);
        assert_eq!(Solution::monotone_increasing_digits(120), 119);
        assert_eq!(Solution::monotone_increasing_digits(1224), 1224);
    }
}
```

## 性能

`Runtime`: 0 ms, faster than 100.00% of Rust online submissions for Monotone Increasing Digits.
`Memory Usage`: 2.3 MB, less than 100.00% of Rust online submissions for Monotone Increasing Digits.

## 思路

从左往右，寻找第一个出现数字递减关系的标号，再往前找第一个递减的数字，这个数字减一，后面全补上9即可

比方说: 1233332221, 对应的应该是122999..., 有比较明显的特点

## 复杂度
考虑到每个数最长不超过10个数字，因此空间和时间复杂度都应该是O(1)

## 提升空间
好像我写的不够简洁

## 困难点
一开始的时候，我没有考虑到数字相同的情况，导致没有找到递减的时候往前回溯

## 分类
贪婪

## 类似题目

1) Jump Game
2) Best Time to Buy and Sell Stock
3) Gas Station
