# 词库转换 示例

说明：将词库编码全拼转换为双拼(此处用小鹤方案)。

## 词库获取

https://pinyin.sogou.com/dict/

## 预处理

深蓝词库转换：https://github.com/studyzy/imewlconverter

将获得的词库转换并稍作编辑得到如下样式的文本文件 ciku.txt：

```
 ben zheng tai	本征态
 bian shi	编时
 bian shi cheng ji	编时乘积
 bian shi suan fu	编时算符
 biao guan fa san	表观发散
 biao guan fa san du	表观发散度
 biao liang chang	标量场
```

行首一个半角空格，每个编码之间相隔一个半角空格，编码与汉字以一个 `tab` 分隔。

## 转换

在终端中执行以下命令（注意部分命令的执行顺序）：

```shell
sed -i 's/ o/ oo/g' ciku.txt
sed -i 's/ e/ ee/g' ciku.txt
sed -i 's/ a/ aa/g' ciku.txt
sed -i 's/ve/t/g' ciku.txt
sed -i 's/uo/o/g' ciku.txt
sed -i 's/un/y/g' ciku.txt
sed -i 's/ui/v/g' ciku.txt
sed -i 's/ue/t/g' ciku.txt
sed -i 's/uang/l/g' ciku.txt
sed -i 's/uan/r/g' ciku.txt
sed -i 's/uai/k/g' ciku.txt
sed -i 's/ua/x/g' ciku.txt
sed -i 's/ou/z/g' ciku.txt
sed -i 's/ong/s/g' ciku.txt
sed -i 's/iu/q/g' ciku.txt
sed -i 's/iong/s/g' ciku.txt
sed -i 's/ing/k/g' ciku.txt
sed -i 's/in/b/g' ciku.txt
sed -i 's/ie/p/g' ciku.txt
sed -i 's/iao/n/g' ciku.txt
sed -i 's/iang/l/g' ciku.txt
sed -i 's/ian/m/g' ciku.txt
sed -i 's/ia/x/g' ciku.txt
sed -i 's/eng/g/g' ciku.txt
sed -i 's/en/f/g' ciku.txt
sed -i 's/ei/w/g' ciku.txt
sed -i 's/ao/c/g' ciku.txt
sed -i 's/ang/h/g' ciku.txt
sed -i 's/an/j/g' ciku.txt
sed -i 's/ai/d/g' ciku.txt
sed -i 's/zh/v/g' ciku.txt
sed -i 's/sh/u/g' ciku.txt
sed -i 's/ch/i/g' ciku.txt

```

得到如下样式的结果：

```
 bf vg td	本征态
 bm ui	编时
 bm ui ig ji	编时乘积
 bm ui sr fu	编时算符
 bn gr fa sj	表观发散
 bn gr fa sj du	表观发散度
 bn ll ih	标量场
```

## 后处理

根据自己需要，再处理，以导入目标输入法。

