sed 是 Linux 系统中非常常用的一个文本处理工具，它可以用来编辑、转换、替换文本文件中的文本。常用的操作包括：文本替换、删除特定行、添加特定行等。以下是 sed 命令常用的选项和语法：

## 选项
-n：只打印模式匹配行（与默认的打印所有行相反）

-i：直接编辑文件，替换原文件中的文本内容

-e：允许对输入数据应用多条 sed 命令（可以使用多个 -e 选项）

## 语法
sed [OPTIONS] 'command' filename 
 
OPTIONS：sed 命令的选项，可以是 -n、-i 或 -e 等

'command'：sed 命令可以是单行或多行，可用多个命令组合称为一个命令列表，多个命令之间用分号 ; 分隔

filename：待处理的文件名或标准输入，可以通过管道从其他命令中读取

## 常用命令
### 替换
sed 's/old/new/g' file      # 将文本文件 file 中所有文本中的 old 替换为 new 
 
sed '/pattern/s/old/new/g' file  # 只替换包含模式 pattern 的行 
 
s 命令用于替换，在第一个斜杠后的字符串是要被替换的部分，第二个斜杠后的字符串是用于替换的内容，g 则表示在每一行中全部替换，而不仅仅是第一个。
### 删除
sed '3d' file                # 删除文本文件 file 的第 3 行 
 
sed '/pattern/d' file        # 只删除包含模式 pattern 的行 
 
d 命令用于删除。
### 添加和插入
sed '1i add_line_text' file # 在文本文件 file 的第 1 行前添加一行文本 
 
sed '/pattern/i add_line_text' file # 在包含模式 pattern 的行前插入一行文本 
 
i 命令用于在指定位置插入一行文本。
以上就是基本的 sed 命令用法介绍，sed 的命令非常广泛，更多使用方法可以通过 man sed 查看 sed 命令的手册。
