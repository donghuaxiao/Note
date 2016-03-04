## Tmux

### 1. Tmux 配置
```
  配置文件路径： ~/.tmux.conf
  
  修改默认的Ctrl + b 为 Ctrl + a
  set-option -g prefix C+a
  unbind C+b
  
  加载配置文件
  tmux source-file ~/.tmux.conf
```

### 2 Tmux 分屏

c+a ; (先按 Ctrl+a, 在按 ; 水平分屏)

c+a %  垂直分屏

c+a+-> (同时按下 Ctrl a, ->), 使分屏分割线 --> 移动

c+a + <-: 分屏分割线 <---- 移动

### 3 tmux session 管理
 . 查看session
    tmux ls
 . 退出 session, detach session
    Ctrl+a d 
 . attach 指定 session
  tmux a -t session-num
