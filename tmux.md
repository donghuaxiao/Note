## Tmux

### 1. Tmux 配置
```
  配置文件路径： ~/.tmux.conf
  
  修改默认的Ctrl + b 为 Ctrl + a
  set-option -g prefix C-a
  unbind-key C-b
  
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

### 4. tmux 关闭windows 重命名
  在tmux 中， window 重命名默认是开启的， 因此当我们给一个window 重命名后， 一操作该window , 该窗口的名称又变成以前一样。要保持命名后的window 名称不变，要关闭 window 重命令
  
  在 ~/.tmux.conf 中添加
```
  set-option -g allow-rename off
```
