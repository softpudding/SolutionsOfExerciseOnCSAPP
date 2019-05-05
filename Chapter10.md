# 第10章：系统级I/O
## 练习题
### 10.2
```bash
f
```
### 10.3
```bash
o
```
### 10.4
由于函数原型dup2(int oldfd,int newfd)的写法有些让人困惑，这个问题我一度搞不清楚。但是现在我确定应该是：
```c
dup2(5,STDIN_FILENO)
```
### 10.5
```bash
o
```

