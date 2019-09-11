``` rust
struct MyQueue {
    stack1: Vec<i32>,
    stack2: Vec<i32>,
}


/*
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyQueue {

    /** Initialize your data structure here. */
    fn new() -> Self {
        MyQueue {
            stack1: Vec::new(),
            stack2: Vec::new(),
        }
    }

    /** Push element x to the back of queue. */
    fn push(&mut self, x: i32) {
        self.stack1.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    fn pop(&mut self) -> i32 {
        let ret = self.peek();
        self.stack2.pop();
        ret
    }

    /** Get the front element. */
    fn peek(&mut self) -> i32 {
        if self.stack2.is_empty() {
            loop {
                if self.stack1.is_empty() {
                    break;
                }
                self.stack2.push(self.stack1.pop().unwrap());
            }
        }
        self.stack2[self.stack2.len() - 1]
    }

    /** Returns whether the queue is empty. */
    fn empty(&self) -> bool {
        self.stack1.is_empty() && self.stack2.is_empty()
    }
}
```
## Performance

`Runtime`: 0 ms, faster than 100.00% of Rust online submissions for Implement Queue using Stacks.
`Memory Usage`: 2.4 MB, less than 100.00% of Rust online submissions for Implement Queue using Stacks.

## Thought

通过两个栈的话，就能在peek的时候，找第二个栈，如果没有，就从第一个栈把数据倒一次就可以了，让第一个栈中的数据 reverse

## Complexity

对于每次操作来说，时间复杂度O(1), 空间复杂度O(N), 占用N个i32空间

## Improvement
没有使用RefCell来操作&self, 总感觉这个情况下不使用mut而是RefCell的话，就改变了语义。如果使用了，那么我也不用去修改题目本身的接口代码。

## Difficulties and Countermeasures

一开始想要修改&self, 后来看了看题目，发现可以修改接口，棒棒棒

## Classification

Stack / Queue

## Similar Questions

### 1) Implement Stack Using Queues
### 2) Min Stack
### 3) Max Stack
