# 文本处理

## cut
```bash
demo@wsl-1:~$ tldr cut

  cut

  Cut out fields from stdin or files.
  # -c 字符区间
  - Cut out the first sixteen characters of each line of stdin:
    cut -c 1-16 

  - Cut out the first sixteen characters of each line of the given files:
    cut -c 1-16 file

  - Cut out everything from the 3rd character to the end of each line:
    cut -c 3-
# -d 分隔符。搭配 -f 使用
# -f 区域区间/集合
  - Cut out the fifth field of each line, using a colon as a field delimiter (default delimiter is tab):
    cut -d':' -f5

  - Cut out the 2nd and 10th fields of each line, using a semicolon as a delimiter:
    cut -d';' -f2,10

  - Cut out the fields 3 through to the end of each line, using a space as a delimiter:
    cut -d' ' -f3-


demo@wsl-2:~$
```
注意下面的 oct 和1 之间有两个空格。第三个空格和第四个空格之间是空的。空的也占用了一个区域。
```bash
demo@wsl-9:~$ last

wtmp begins Thu Oct  1 12:32:27 2020
demo@wsl-10:~$ last | cut -d ' ' -f 3

Thu
demo@wsl-11:~$ last | cut -d ' ' -f 4

Oct
demo@wsl-12:~$ last | cut -d ' ' -f 5


demo@wsl-13:~$ last | cut -d ' ' -f 6

1
demo@wsl-14:~$ last | cut -d ' ' -f 7

12:32:27
demo@wsl-15:~$ last | cut -d ' ' -f 8

2020
demo@wsl-16:~$
```

## grep

> Usage: grep [OPTION]... PATTERNS [FILE]...

```bash
demo@wsl-16:~$ tldr grep

  grep

  Matches patterns in input text. 标准输入/文件
  Supports simple patterns and regular expressions.

  - Search for a pattern within a file:
    grep search_pattern path/to/file
# -F ???
  - Search for an exact string:
    grep -F exact_string path/to/file
# -R 递归 -I 忽略非文本文件 -n 显示匹配的行号
  - Search for a pattern [R]ecursively in the current directory, showing matching line [n]umbers, [I]gnoring non-text files:
    grep -RIn search_pattern .
# -i 忽略大小写 -E 支持扩展的正则表达式
  - Use extended regular expressions (supporting ?, +, {}, () and |), in case-insensitive mode:
    grep -Ei search_pattern path/to/file
# -C|B|A 3 或-C3|B3|A3 扩展显示。 如C3，一个孤立的结果能显示7行。A3，显示4行
  - Print 3 lines of [C]ontext around, [B]efore, or [A]fter each match:
    grep -C|B|A 3 search_pattern path/to/file
# -H 匹配的行前面显示文件名。结果显示，文件名是在序号前面的（-nH / -Hn）
  - Print file name with the corresponding line number for each match:
    grep -Hn search_pattern path/to/file

  - Use the standard input instead of a file:
    cat path/to/file | grep search_pattern
# 输出不匹配的结果
  - In[v]ert match for excluding specific strings:
    grep -v search_pattern
    
# -a 以文本文件方式搜索二进制文件
    grep -a search_pattern file

demo@wsl-17:~$
```
