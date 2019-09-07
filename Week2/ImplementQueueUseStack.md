``` rust
struct Stack<T: Sized + Copy> {
    len: usize,
    mem: Vec<T>,
}

impl<T: Sized + Copy> Stack<T> {
    fn new() -> Self {
        Stack {
            len: 0,
            mem: Vec::new(),
        }
    }

    fn is_empty(&self) -> bool {
        self.len == 0
    }

    fn push(&mut self, x: T) {
        self.mem.push(x);
        self.len += 1;
    }

    fn top(&self) -> Option<T> {
        if self.is_empty() {
            None
        } else {
            let x = self.mem[self.len - 1].clone();
            Some(x)
        }
    }

    fn pop(&mut self) {
        if self.is_empty() == false {
            self.mem.pop();
            self.len -= 1;
        }
    }
}


struct MyQueue {
    stack1: Stack<i32>,
    stack2: Stack<i32>,
}


/*
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl MyQueue {

    /** Initialize your data structure here. */
    fn new() -> Self {
        MyQueue {
            stack1: Stack::new(),
            stack2: Stack::new(),
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
                self.stack2.push(self.stack1.top().unwrap());
                self.stack1.pop();
            }
        }
        self.stack2.top().unwrap_or(0)
    }

    /** Returns whether the queue is empty. */
    fn empty(&self) -> bool {
        self.stack1.is_empty() && self.stack2.is_empty()
    }
}

/*
 * Your MyQueue object will be instantiated and called as such:
 * let obj = MyQueue::new();
 * obj.push(x);
 * let ret_2: i32 = obj.pop();
 * let ret_3: i32 = obj.peek();
 * let ret_4: bool = obj.empty();
 */

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_stack() {
        let mut stack: Stack<i32> = Stack::new();
        assert_eq!(stack.is_empty(), true);
        stack.push(1);
        stack.push(2);
        assert_eq!(stack.top(), Some(2));
        stack.push(3);
        stack.push(4);
        stack.pop();
        stack.pop();
        assert_eq!(stack.top(), Some(2));
    }

    #[test]
    fn test_queue() {
        let mut queue = MyQueue::new();
        queue.push(1);
        assert_eq!(queue.peek(), 1);
        queue.push(2);
        assert_eq!(queue.pop(), 1);
    }
}
```
