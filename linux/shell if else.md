1. 数值比较
   
| 比较   | 描述  |
|  ----  | ----  |
| n1 -eq n2  | 检查n1是否与n2相等 |
| n1 -ge n2  | 检查n1是否大于或等于n2 |
| n1 -gt n2  | 检查n1是否大于n2 |
| n1 -le n2  | 检查n1小于或等于n2 |
| n1 -lt n2  | 检查n1是否小于n2 |
| n1 -ne n2  | 检查n1不等于n2 |

2. 字符串比较
   
| 比较   | 描述  |
|  ----  | ----  |
| str1 = str2  | 检查str1是否和str2相同 |
| str1 != str2  | 检查str1是否和str2不同 |
| str1 < str2  | 检查str1是否小于str2,ASCII比较 |
| str1 > str2  | 检查str1是否大于str2,ASCII比较|
| -n str1  | 检查str1的长度是否为非0|
| -z str1  | 检查str1的长度是否为0 |

3. 文件比较
   
| 比较   | 描述  |
|  ----  | ----  |
| -d file | 检查file对象是否存在并是一个目录 |
| -e file | 检查file对象是否存在 |
| -f file  | 检查file对象是否存在并是一个文件 |
| -r file | 检查file对象是否存在并可读 |
| -s file | 检查file是否存在并非空 |
| -w file | 检查file对象是否存在并可写 |
| -x file | 检查file对象是否存在并可执行 |
| -r file | 检查file对象是否存在并可读 |
| -O file | 检查file对象是否存在并属于当前用户所有 |
| -G file | 检查file对象是否存在并默认组与当前用户组相同 |
| file1 -nt file2 | 检查file1是否比file2新 |
| file1 -ot file2 | 检查file1是否比file2旧 |

4. 复合条件测试
   
模版
```
[ condition1 ] && [ condition2 ] 
[ condition1 ] || [ condition2 ] 
```
test.sh
``` 
#!/bin/bash
if [ ! -d $HOME ] && [ -w $HOME/testing ];then
      echo "1"
else 
      echo "2"
fi
```
5.使用双括号((...))
| 比较   | 描述  |
|  ----  | ----  |
| val++ | 后增 |
| val-- | 后减 |
| ++val | 先增 |
| --val | 先减 |
| ** | 幂运算 |
| << | 左位移 |
| >> | 右位移 |
| ~ | 位求反 |
| & | 位和 |
| \| | 位与 |
| ! | 逻辑求反 |
| && | 逻辑和 |
| \|\| | 逻辑与 |
6.使用双方括号[[ ... ]]
字符串比较高级特性
``` test.sh
#!/bin/bash
if [[ $USER == r* ]];then
    echo "Hello $USER"
else
    echo "Sorry,I do not know you."
fi
```
sh test.sh

`Hello rich`

7. case

case模版：
``` 
case var in 
pattern1 | pattern2) 
   commands1;;
pattern3)
   commands2;;
*)
   default commands;;
esac
```
test.sh
``` 
case $USER in
rich | apple)
    echo "enjoy your visit.";;
tesing)
    echo "testing your code";;
online)
    echo "put your code online";;
*)
    echo "Sorry,you are not allowed here";;
esac
```