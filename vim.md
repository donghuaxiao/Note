# Vim 笔记
## 1. Vim 创建文件时添加文本

```vim
function HeaderPython()
     call setline(1, "#!/usr/bin/env python")
      call append(1,"# -*- coding:utf-8 -*-")
      normal G
      normal o
 endf
 autocmd bufnewfile *.py call HeaderPython()
```

## 2. Vim map 命令
- 使用代码缩写， 在插入模式下， 输入 sout , 被替换成 System.out.println();
```
imap sout System.out.println();
```
 - 运行Python 程序
 ```
 map <F4> :w<CR> :!python %<CR>
 ```
