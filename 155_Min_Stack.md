[题目介绍](https://leetcode.com/problems/min-stack/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

 

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```



### 解法

两个栈来实现这个功能，但是感觉有些奇怪。

```
class MinStack {
private:
    stack<int> st1; 
    stack<int> st2;
public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        st1.push(x);
        if(st2.empty() || x <= getMin()){
            st2.push(x);
        }
    }
    
    void pop() {
        if(st1.top() == getMin()){
            st2.pop();
        }
        st1.pop();
        
    }
    
    int top() {
        return st1.top();
        
    }
    
    int getMin() {
        return st2.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```



用一个栈来实现，内容是pair对，存放当前push的内容和最小值的pair对。

```
class MinStack {
private:
    stack<pair<int, int>> st;

public:
    /** initialize your data structure here. */
    MinStack() {
        
    }
    
    void push(int x) {
        int min;
        if (st.empty()) {
            min = x;
        }
        else {
            min = std::min(st.top().second,x);
        }
        st.push({x, min});
    }

    void pop() {
        st.pop();
    }

    int top() {
        return st.top().first;
    }

    int getMin() {
        return st.top().second;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```

