```rust
impl Solution {
    fn visit(res: &mut Vec<Vec<i32>>, cur_path: &mut Vec<i32>, visited: &mut Vec<i32>, node: i32, target: i32, graph: &Vec<Vec<i32>>) {
        if node == target {
            res.push(cur_path.clone());
            return;
        }
        for nd in &graph[node as usize] {
            let nd: i32 = *nd;
            if visited[nd as usize] == 1 {
                continue;
            }
            visited[nd as usize] = 1;
            cur_path.push(nd);
            Solution::visit(res, cur_path, visited, nd, target, graph);
            cur_path.pop();
            visited[nd as usize] = 0;
        }
    }
    pub fn all_paths_source_target(graph: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let mut res: Vec<Vec<i32>> = Vec::new();
        let mut cur_path = Vec::new();
        let mut visited: Vec<i32> = Vec::new();
        visited.resize(graph.len(), 0);
        let target = (graph.len() - 1) as i32;
        visited[0] = 1;
        cur_path.push(0);
        Solution::visit(&mut res, &mut cur_path, &mut visited, 0, (graph.len()-1) as i32, &graph);
        res
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn it_works() {
        assert_eq!(Solution::all_paths_source_target(vec![vec![1,2],vec![3],vec![3],vec![]]), vec![vec![0,1,3],vec![0,2,3]]);
    }
}

```

## 性能

执行用时 :12 ms, 在所有 Rust 提交中击败了94.44%的用户
内存消耗 :2.5 MB, 在所有 Rust 提交中击败了100.00%的用户

## 思路

广度优先

## 复杂度
对于图 (V, E)

时间复杂度: O(E + V), 对于每个节点，每条边，都会访问一次
空间复杂度: O(V), 一个buf至多存储V个节点

## 提升空间
暂无

## 困难点

没有什么困难

## 分类
图

## 类似题目

1) [`Clone Graph`](https://leetcode-cn.com/problems/clone-graph/)
2) [`The Maze`](https://leetcode-cn.com/problems/the-maze/)
3) [`Bus Routes`](https://leetcode-cn.com/problems/bus-routes/)
