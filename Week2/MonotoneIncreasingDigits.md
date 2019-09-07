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
