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

## sort

```bash
demo@wsl-2:~$ sort --help
Usage: sort [OPTION]... [FILE]...
  or:  sort [OPTION]... --files0-from=F
Write sorted concatenation of all FILE(s) to standard output.

With no FILE, or when FILE is -, read standard input.
```


```bash
demo@wsl-1:~$ tldr sort

  sort

  Sort lines of text files.
  More information: https://www.gnu.org/software/coreutils/manual/html_node/sort-invocation.html.

# 默认 升序
  - Sort a file in ascending order:
    sort path/to/file
# -r 降序
  - Sort a file in descending order:
    sort --reverse path/to/file
# -i 忽略大小写
  - Sort a file in case-insensitive way:
    sort --ignore-case path/to/file
# -n 数字顺序 !!! 非字母顺序。比如 文件夹排序 1_dir 21_dir 31_dir 111_dir 121_dir 131_dir 21_dir1 221_dir 231_dir
  - Sort a file using numeric rather than alphabetic order:
    sort --numeric-sort path/to/file
# -t '分隔符'，默认是 tab .  -k 排序区间域
  - Sort /etc/passwd by the 3rd field of each line numerically, using ":" as a field separator:
    sort --field-separator=: --key=3n /etc/passwd
    例 cat /etc/passwd | sort -t ':' -k 3   排序涉及第三区域及其后的内容
       cat /etc/passwd | sort -t ':' -k 3,3 单纯以第三区域内容排序
# 像同的内容，只出现一次
  - Sort a file preserving only unique lines:
    sort --unique path/to/file
# -o 输出到文件
  - Sort a file, printing the output to the specified output file (can be used to sort a file in-place):
    sort --output=path/to/file path/to/file
# ？？？
  - Sort numbers with exponents:
    sort --general-numeric-sort path/to/file
# -b 忽略前面空白部分 ignore leading blanks
# -f 忽略大小写 fold lower case to upper case characters
# -i --ignore-nonprinting    consider only printable characters
demo@wsl-2:~$
```

## uniq 

```bash
Usage: uniq [OPTION]... [INPUT [OUTPUT]]
Filter adjacent matching lines from INPUT (or standard input),
writing to OUTPUT (or standard output).

With no options, matching lines are merged to the first occurrence.
```

```bash
demo@wsl-4:~$ tldr uniq

  uniq

  Output the unique lines from the given input or file.
  Since it does not detect repeated lines unless they are adjacent, we need to sort them first. 只能检测到相邻的相同行，因此需要先排序
# sort 过程，空行是也参与排序的
  - Display each line once:
    sort file | uniq
# 只显示没有重复的行
  - Display only unique lines:
    sort file | uniq -u
# 只显示有重复的行 
  - Display only duplicate lines:
    sort file | uniq -d
# 上面两个输出结果的交是全集

# 在每一行的行首显示出现次数
  - Display number of occurrences of each line along with that line:
    sort file | uniq -c

  - Display number of occurrences of each line, sorted by the most frequent:
    sort file | uniq -c | sort -nr


demo@wsl-5:~$
```

