# Vim 笔记
## 1. Vim 创建文件时添加文本
`function HeaderPython()
     call setline(1, "#!/usr/bin/env python")
      call append(1,"# -*- coding:utf-8 -*-")
      normal G
      normal o
  endf
  autocmd bufnewfile *.py call HeaderPython()

`
