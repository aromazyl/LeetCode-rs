```rust
impl Solution {
    pub fn reverse_string(s: &mut Vec<char>) {
        if s.len() == 0 {
            return;
        }
        let mut i = 0;
        let mut j = s.len() - 1;
        while i < j {
            s[i] = ((s[i] as u8) ^ (s[j] as u8)) as char;
            s[j] = ((s[i] as u8) ^ (s[j] as u8)) as char;
            s[i] = ((s[i] as u8) ^ (s[j] as u8)) as char;
            i += 1;
            j -= 1;
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_solution() {
        let mut test_vec = vec!['1','2','3','4','5'];
        Solution::reverse_string(&mut test_vec);
        assert_eq!(test_vec, vec!['5', '4', '3', '2', '1']);
        test_vec = vec![];
        assert_eq!(test_vec, vec![]);
        test_vec = vec!['1'];
        assert_eq!(test_vec, vec!['1']);
    }
}

```

## 性能

Runtime: 20 ms, faster than 97.62% of Rust online submissions for Reverse String.
Memory Usage: 5 MB, less than 100.00% of Rust online submissions for Reverse String.

## 思路

从两边到中间，利用bit计算来换位置即可

## 复杂度

时间复杂度O(N), 空间复杂度O(1)

## 提升空间
并没有, performance比直接调用reverse更快!!

## 困难点

没有什么困难

## 分类
Two Pointers; String

## 类似题目

1) Reverse Vowels of a String
2) Reverse String II
3) Two Sum
