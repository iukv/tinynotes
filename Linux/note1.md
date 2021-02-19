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



## 

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

## wc

```bash
demo@wsl-13:~$ tldr wc

  wc

  Count lines, words, or bytes.

  - Count lines in file:
    wc -l file

  - Count words in file:
    wc -w file

  - Count characters (bytes) in file:
    wc -c file

  - Count characters in file (taking multi-byte character sets into account):
    wc -m file

  - Use standard input to count lines, words and characters (bytes) in that order:
    find . | wc


demo@wsl-14:~$
```

``` bash
demo@wsl-18:~$ tldr wc | wc ; tldr wc | wc -l; tldr wc | wc -w ; tldr wc | wc -c ; tldr wc | wc -m
     21      63     371
21
63
371
371
demo@wsl-19:~$
```

## tee

### 10.6.3 雙向重導向： [tee](https://linux.vbird.org/linux_basic/centos7/0320bash.php#pipe)

想個簡單的東西，我們由前一節知道 > 會將資料流整個傳送給檔案或裝置，因此我們除非去讀取該檔案或裝置， 否則就無法繼續利用這個資料流。萬一我想要將這個資料流的處理過程中將某段訊息存下來，應該怎麼做？ 利用 tee 就可以囉～我們可以這樣簡單的看一下：

![tee 的工作流程示意圖](https://linux.vbird.org/linux_basic/centos7/0320bash//0320bash_5.png "tee 的工作流程示意圖")

圖10.6.2、tee 的工作流程示意圖

```bash
demo@wsl-27:~$ tldr tee

  tee

  Read from standard input and write to standard output and files (or commands).

  - Copy standard input to each FILE, and also to standard output:
    echo "example" | tee FILE
    # 同时导入到多个文件 （若文件包存在会创建）：
    echo "example" | tee FILE1 FILE2 FILE3 
    
    # 从键盘同时输入到多个文件
    tee file1 file2 file3
      然后会同 cat file1 一样，从键盘输入。
    
# -a 追加
  - Append to the given FILEs, do not overwrite:
    echo "example" | tee -a FILE
    
   [dmtsai@study ~]$ ls -l /home | tee ~/homefile | more
    # 這個範例則是將 ls 的資料存一份到 ~/homefile ，同時螢幕也有輸出訊息！

  - Print standard input to the terminal, and also pipe it into another program for further processing:
    echo "example" | tee /dev/tty | xargs printf "[%s]"
# 
  - Create a directory called "example", count the number of characters in "example" and write "example" to the terminal:
    echo "example" | tee >(xargs mkdir) >(wc -c)


demo@wsl-28:~$
```

info tee

```bash
$  wget -O - https://example.com/dvd.iso \
       | tee >(sha1sum > dvd.sha1) > dvd.iso
       
$ wget -O - https://example.com/dvd.iso \
       | tee dvd.iso | sha1sum > dvd.sha1
       
$ wget -O - https://example.com/dvd.iso \
       | tee >(sha1sum > dvd.sha1) \
             >(md5sum > dvd.md5) \
       > dvd.iso
```


## tr

```bash

  tr
# 字符替换、删除、转换：基于单个字符或字符串。
  Translate characters: run replacements based on single characters and character sets.
  
# 从文件输入，再输出到屏幕
  - Replace all occurrences of a character in a file, and print the result:
    tr find_character replace_character < filename

# 从管道输入
  - Replace all occurrences of a character from another command's output:
    echo text | tr find_character replace_character

# 将第一个字符集的每个字符映射到第二个字符集的对应字符： 
  - Map each character of the first set to the corresponding character of the second set:
    tr 'abcd' 'jkmn' < filename
    last | tr '[a-z]' '[A-Z]' #单引号可省略
# -d 删除特定字符    
  - Delete all occurrences of the specified set of characters from the input:
    tr -d 'input_characters' < filename

  - Compress a series of identical characters to a single character:
    tr -s 'input_characters' < filename

# tr 的搜寻方式兼容正则表达式， 如
  - Translate the contents of a file to upper-case:
    tr "[:lower:]" "[:upper:]" < filename
    
  - Strip out non-printable characters from a file:
    tr -cd "[:print:]" < filename
    
    ```
    
## col
过滤控制字符

```bash

[dmtsai@study ~]$ col [-xb]
選項與參數：
-x  ：將 tab 鍵轉換成對等的空白鍵

範例一：利用 cat -A 顯示出所有特殊按鍵，最後以 col 將 [tab] 轉成空白
[dmtsai@study ~]$ cat -A /etc/man_db.conf  <==此時會看到很多 ^I 的符號，那就是 tab
[dmtsai@study ~]$ cat /etc/man_db.conf | col -x | cat -A | more

```

> 嘿嘿！如此一來， [tab] 按鍵會被取代成為空白鍵，輸出就美觀多了！
> 雖然 col 有他特殊的用途，不過，很多時候，他可以用來簡單的處理將 [tab] 按鍵取代成為空白鍵！ 例如上面的例子當中，如果使用 cat -A 則 [tab] 會以 ^I 來表示。 但經過 col -x 的處理，則會將 [tab] 取代成為對等的空白鍵！
> 

## join

```bash
demo@wsl-6:~$ tldr join

  join
  接合后的文件，其参照栏位为合并成一个并出现在行首。
  
# 接合两个经过sort整理过的文件
  Join lines of two **sorted** files on a common field.
  
# 默认以第一栏位识别
  - Join two files on the first (default) field:
    join file1 file2
    
# 自定义栏位的分隔符
  - Join two files using a comma (instead of a space) as the field separator:
    join -t ',' file1 file2
    
# 分别自定义两个文件进行接合所参照的栏位
  - Join field3 of file1 with field1 of file2:
    join -1 3 -2 1 file1 file2

  - Produce a line for each unpairable line for file1:
    join -a 1 file1 file2


demo@wsl-7:~$
```

## paste

```bash
demo@wsl-8:~$ tldr paste

  paste
  Merge lines of files.
  
Usage: paste [OPTION]... [FILE]...
Write lines consisting of the sequentially corresponding lines from
each FILE, separated by TABs, to standard output.

With no FILE, or when FILE is -, read standard input.

Mandatory arguments to long options are mandatory for short options too.
  -d, --delimiters=LIST   reuse characters from LIST instead of TABs
  -s, --serial            paste one file at a time instead of in parallel 一次只读取一个文件的，第一个文件结束后，读取第二个文件
  -z, --zero-terminated    line delimiter is NUL, not newline
      --help     display this help and exit
      --version  output version information and exit


# 把单格文件的所有行合并为一行。
  # 默认以tab 分隔
  - Join all the lines into a single line, using TAB as delimiter:
    paste -s file
  # 自定义分隔符
  - Join all the lines into a single line, using the specified delimiter:
    paste -s -d delimiter file
  # 合并两个文件 直接左右并列
  - Merge two files side by side, each in its column, using TAB as delimiter:
    paste file1 file2
    
  - Merge two files side by side, each in its column, using the specified delimiter:
    paste -d delimiter file1 file2
  # 以 \n（换行） 作为分隔符。如交替列印 控制字符要用引号括起来。
  - Merge two files, with lines added alternatively:
    paste -d '\n' file1 file2


demo@wsl-9:~$
```

另外请 参阅 info paste


## expand

```bash
demo@wsl-41:~$ tldr expand

  expand

  Convert tabs to spaces. #默认8个空格

  - Convert tabs in each file to spaces, writing to standard output:
    expand file

  - Convert tabs to spaces, reading from standard input:
    expand
    
# 只转换行首的tab
  - Do not convert tabs after non blanks:
    expand -i file
    
# 自定义空格个数
  - Have tabs a certain number of characters apart, not 8:
    expand -t=number file

# ????
  - Use a comma separated list of explicit tab positions:
    expand -t=1,4,6


demo@wsl-42:~$
```

##xargs 

[vbird](https://linux.vbird.org/linux_basic/centos7/0320bash.php#pipe:~:text=10.6.6%20%E5%8F%83%E6%95%B8,%E6%8F%9B%EF%BC%9A%20xargs)



## grep 进阶

···
--color=auto 会匹配结果会显示颜色

dmesg | grep -n -A3 -B2 --color=auto 'qxl'
匹配结果及其后三行前两行，并显示颜色
···

```bash
grep 搜做内容表达式示例

特定字串
'the'
't[ae]st'

集和字元
'oo'
'[^g]oo'
 '[^a-z]oo'
 
 '[0-9]'
 '[^[:lower:]]oo'
 
 行首行尾
'^the'
'^[a-z]'
'^[[:lower:]]'
'^[^a-zA-Z]'
'\.$'  行尾的点
'^$'  空行

'o\{2\}' 搜索oo
'go\{2,5\}g'  2~5个o
'go\{2,\}g'

```

RE [字符汇总](https://linux.vbird.org/linux_basic/centos7/0330regularex.php#sed:~:text=11.2.4%20%E5%9F%BA%E7%A4%8E%E6%AD%A3%E8%A6%8F,%E5%AD%97%E7%AC%A6%E5%BD%99%E6%95%B4%20(characters))

```
基础的 用grep
^word
word$
.
\
*
[list]
[n1-n2]
[^list]
\{n,m\}

扩展的 用 egrep 或 grep -E
+
?
|
()     # egrep -n 'g(la|oo)d' regular_express.txt
()+    #echo 'AxyzxyzxyzxyzC' | egrep 'A(xyz)+C'



# 搜索特殊字符的转义 grep 和 egrep 的特殊字符是不同的。是否需要看情况。
  .*[]搜索字面内容要转义
  {} 用来限定范围要转义。搜索其字面意思不用转义。

  （ grep 不需要转义，egrep 需要 ……

  ！ 和 > 不需要转义
  grep -n '[!>]' regular_express.txt

```

选项
```bash
-i
-v
-n
-c 输出匹配到的个数
-a 將 binary 檔案以 text 檔案的方式搜尋資料
-H 行首显示文件
--color=auto 突出显示匹配结果
```

## sed

[ref](https://linux.vbird.org/linux_basic/centos7/0330regularex.php#sed)

```bash
demo@wsl-2:~$ tldr sed

  sed
  sed [-nefr] [動作]

-n  ：使用安靜(silent)模式。在一般 sed 的用法中，所有來自 STDIN 的資料一般都會被列出到螢幕上。
      但如果加上 -n 參數後，則只有經過 sed 特殊處理的那一行(或者動作)才會被列出來。
-e  ：直接在指令列模式上進行 sed 的動作編輯；
-f  ：直接將 sed 的動作寫在一個檔案內， -f filename 則可以執行 filename 內的 sed 動作；
-r  ：sed 的動作支援的是延伸型正規表示法的語法。(預設是基礎正規表示法語法)
-i  ：直接修改讀取的檔案內容，而不是由螢幕輸出。

動作說明：  [n1[,n2]]function
n1, n2 ：不見得會存在，一般代表『選擇進行動作的行數』，舉例來說，如果我的動作
         是需要在 10 到 20 行之間進行的，則『 10,20[動作行為] 』

function 有底下這些咚咚：
a   ：新增， a 的後面可以接字串，而這些字串會在新的一行出現(目前的下一行)～
c   ：取代， c 的後面可以接字串，這些字串可以取代 n1,n2 之間的行！
d   ：刪除，因為是刪除啊，所以 d 後面通常不接任何咚咚；
i   ：插入， i 的後面可以接字串，而這些字串會在新的一行出現(目前的上一行)；
p   ：列印，亦即將某個選擇的資料印出。通常 p 會與參數 sed -n 一起運作～
s   ：取代，可以直接進行取代的工作哩！通常這個 s 的動作可以搭配正規表示法！
      例如 1,20s/old/new/g 就是啦！
      
  Edit text in a scriptable manner.

  - Replace the first occurrence of a regular expression in each line of a file, and print the result:
    sed 's/regex/replace/' filename
    
  - Replace all occurrences of an extended regular expression in a file, and print the result:
    sed -r '3,5s/regex/replace/g' filename  # 3到5行取代   #  -E, -r, --regexp-extended

  - Replace all occurrences of a string in a file, overwriting the file (i.e. in-place):
    sed -i 's/find/replace/g' filename # -i 直接编辑原文件

  - Replace only on lines matching the line pattern:
    sed '/line_pattern/s/find/replace/' filename   # 匹配特定行进行匹配

  - Delete lines matching the line pattern:
    sed '/line_pattern/d' filename  # 匹配特定行删除
    
# q [EXIT-CODE]打印到11行，然后退出。 Exit 'sed' without processing any more commands or input.
  - Print the first 11 lines of a file:
    sed 11q filename
# 对 filename 连续进行量词操作。 -e 可 与 -f 等效，如下
  - Apply multiple find-replace expressions to a file:
    sed -e 's/find/replace/' -e 's/find/replace/' filename
    
    echo 's/find/replace/' > file1.sed
    echo  's/find/replace/' > file2.sed
    sed -f file1.sed -f file2.sed filename

# 特此看情况下，s/ / / ，可把/替换为其他字符
  - Replace separator / by any other character not used in the find or replace patterns, e.g., #:
    sed 's#find#replace#' filename


demo@wsl-3:~$
```

info sed

```bash
'#'
     [No addresses allowed.]

     The '#' character begins a comment; the comment continues until the
     next newline.

     If you are concerned about portability, be aware that some
     implementations of 'sed' (which are not POSIX conforming) may only
     support a single one-line comment, and then only when the very
     first character of the script is a '#'.

     Warning: if the first two characters of the 'sed' script are '#n',
     then the '-n' (no-autoprint) option is forced.  If you want to put
     a comment in the first line of your script and that comment begins
     with the letter 'n' and you do not want this behavior, then be sure
     to either use a capital 'N', or place at least one space before the
     'n'.
     
     若表达式写在文件里，且第一行为注释，且#后第一个字母为n, 即#n... ，则，n可能被视位 选择了 -n, 根据情况自行避免。
     
     
     
'q [EXIT-CODE]'  列印至某行后停止进行
     Exit 'sed' without processing any more commands or input.

     Example: stop after printing the second line:
          $ seq 3 | sed 2q
          1
          2

     This command accepts only one address.  Note that the current
     pattern space is printed if auto-print is not disabled with the
     '-n' options.  The ability to return an exit code from the 'sed'
     script is a GNU 'sed' extension.

     See also the GNU 'sed' extension 'Q' command which quits silently
     without printing the current pattern space.
     
'd' 删除
     Delete the pattern space; immediately start next cycle.

     Example: delete the second input line:
          $ seq 3 | sed 2d  # 删除第二行 。 另如2到5行： 2,5d
          1
          3

'p' 列印
     Print out the pattern space (to the standard output).  This command
     is usually only used in conjunction with the '-n' command-line
     option.  # 与 -n 搭配，避免重复输出

     Example: print only the second input line:
          $ seq 3 | sed -n 2p
          2

'n'
     If auto-print is not disabled, print the pattern space, then,
     regardless, replace the pattern space with the next line of input.
     If there is no more input then 'sed' exits without processing any
     more commands.

     This command is useful to skip lines (e.g.  process every Nth
     line).

     Example: perform substitution on every 3rd line (i.e.  two 'n'
     commands skip two lines):  两个n 标势把 . 所匹配内容替换成 x，如此进行
          $ seq 6 | sed 'n;n;s/./x/'
          1
          2
          x
          4
          5
          x

     GNU 'sed' provides an extension address syntax of FIRST~STEP to
     achieve the same result:

          $ seq 6 | sed '0~3s/./x/'
          1
          2
          x
          4
          5
          x

'{ COMMANDS }'
     A group of commands may be enclosed between '{' and '}' characters.
     This is particularly useful when you want a group of commands to be
     triggered by a single address (or address-range) match.

     Example: perform substitution then print the second input line:
          $ seq 3 | sed -n '2{s/2/X/ ; p}'
          X


'y/SOURCE-CHARS/DEST-CHARS/'  字符一对一转换，类似于 tr   
     Transliterate any characters in the pattern space which match any
     of the SOURCE-CHARS with the corresponding character in DEST-CHARS.

     Example: transliterate 'a-j' into '0-9':
          $ echo hello world | sed 'y/abcdefghij/0123456789/'
          74llo worl3

     (The '/' characters may be uniformly replaced by any other single
     character within any given 'y' command.)

     Instances of the '/' (or whatever other character is used in its
     stead), '\', or newlines can appear in the SOURCE-CHARS or
     DEST-CHARS lists, provide that each instance is escaped by a '\'.
     The SOURCE-CHARS and DEST-CHARS lists _must_ contain the same
     number of characters (after de-escaping).

     See the 'tr' command from GNU coreutils for similar functionality.


'a','c','i' (append/change/insert)

'a TEXT' 在指定行后添加 'i TEXT' 是在前一行添加。
  a后的空被忽略，如需，可转义 '\ '
     Appending TEXT after a line.  This is a GNU extension to the
     standard 'a' command - see below for details.

     Example: Add the word 'hello' after the second line:
          $ seq 3 | sed '2a hello'
          1
          2
          hello
          3

 As a GNU extension, this command accepts two addresses.

     Escape sequences in TEXT are processed, so you should use '\\' in
     TEXT to print a single backslash.

     The commands resume after the last line without a backslash ('\') -
     'world' in the following example:  添加内容可分成几行
          $ seq 3 | sed '2a\
          hello\
          world
          3s/./X/'
          -|1
          -|2
          -|hello
          -|world
          -|X

     As a GNU extension, the 'a' command and TEXT can be separated into
     two '-e' parameters, enabling easier scripting: 
          $ seq 3 | sed -e '2a\' -e hello
          1
          2
          hello
          3

          $ sed -e '2a\' -e "$VAR" 添加内容可分离出来单独设置为变量。


demo@wsl-72:~$ seq 10 | sed '2,9c hello'  # c 取代，2~9行整体取代
1
hello
10
demo@wsl-73:~$ seq 10 | sed '2,9s/.*/hello/g'  按行取代
1
hello
hello
hello
hello
hello
hello
hello
hello
10
demo@wsl-74:~$

     $ seq 6 | sed '1d  #删除不连续的指定行
     3d
     5d'
     2
     4
     6
     
     $ seq 6 | sed -e 1d -e 3d -e 5d
     2
     4
     6


     $ seq 6 | sed -e 1d -e 3d -e 5d
     2
     4
     6



# sed 'function1
function2'

# sed -e function1 -e function2
sed -e 'function1' -e 'function2'

如若涉及到特定行，则是一句初始文件的行的编号而定

'a','c','i' (append/change/insert)

     All characters following 'a','c','i' commands are taken as the text
     to append/change/insert.  Using a semicolon leads to undesirable
     results:

          $ seq 2 | sed '1aHello ; 2d'
          1
          Hello ; 2d
          2

     Separate the commands using '-e' or a newline:

          $ seq 2 | sed -e 1aHello -e 2d
          1
          Hello

          $ seq 2 | sed '1aHello
          2d'
          1
          Hello

     Note that specifying the text to add ('Hello') immediately after
     'a','c','i' is itself a GNU 'sed' extension.  A portable,
     POSIX-compliant alternative is:

          $ seq 2 | sed '1a\
          Hello
          2d'
          1
          Hello


  The following examples are all equivalent.  They perform two 'sed'
operations: deleting any lines matching the regular expression '/^foo/',
and replacing all occurrences of the string 'hello' with 'world':

     sed '/^foo/d ; s/hello/world/' input.txt > output.txt

     sed -e '/^foo/d' -e 's/hello/world/' input.txt > output.txt

     echo '/^foo/d' > script.sed
     echo 's/hello/world/' >> script.sed
     sed -f script.sed input.txt > output.txt

     echo 's/hello/world/' > script2.sed
     sed -e '/^foo/d' -f script2.sed input.txt > output.txt


3.3 The 's' Command
===================

The 's' command (as in substitute) is probably the most important in
'sed' and has a lot of different options.  The syntax of the 's' command
is 's/REGEXP/REPLACEMENT/FLAGS'.

The 's' command can be followed by zero or more of the following
FLAGS:

'g'
     Apply the replacement to _all_ matches to the REGEXP, not just the
     first.

'NUMBER'
     Only replace the NUMBERth match of the REGEXP.



sed '1,5s/$/ F F F/g' 在1-5行行内末尾添加内容 


```


