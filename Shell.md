##Shell

### 1. Shell 分隔符
内部自字段分割符(Internal Field Separator, IFS) 是shell 脚本中的一个特殊变量，用来把分割一行数据分割成多个数据。 IFS是存储分隔符的环境变量，默认值为空白字符（换行符,制表符，空格)

迭代一个字符串：

	#!/bin/bash

	data="123,222,333,444,555,666"
	
	oldIFS=$IFS
	IFS=,
	for i in $data
	do
		echo $i
	done
	
	IFS=$oldIFS

执行结果：

	123
	222
	333
	444
	555
	666
	
也可以通过把，替换为空格符，然后在迭代：
	
	data=$(echo $data | sed 's/,/ /g')
	for i in $data
	do
		deal with $i
	done

使用tr 把, 转换成空格

	data=$(echo $data | tr ',' ' ')
	for i in $data
	do
		deal with $i
	done


### 2 Shell 脚本调试

#### 1). 使用选项 -x
	
	bash -x script.sh

#### 2). 使用set +/-x; set +/-v

* set -x：  在执行时候显示参数和命令
* set +x： 禁止调试
* set -v: 当命令进入读取时显示输入
* set +v : 禁止打印输入