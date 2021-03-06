# 五、Bash基本使用
## 1.read命令：
   1）定义：   
   read命令是用于从终端或者文件中读取输入的内部命令。
   读取整行输入。
   每行末尾的换行符不被读入。
   
   2）read命令使用
   - 从标准输入读取输入并赋值给变量
   - read var
   - 从标准输入读取多个内容
   - read var1 var2 var3
   - 不指定变量（默认赋值给REPLY）

  3）脚本参数传递
  - $0 脚本名称
  - $1~$n 获取参数
  - $# 传递到脚本的参数个数
  - $$ 脚本运行的当前进程的ID号
  - $* 以一个单字符串显示所有向脚本传递的参数
  - $?显示最后命令的退出状态。0表示没有错误，其他任何值表明有错误

## 2.基本运算

  1）算数运算1
  
a=10 b=20
     
   ① +：加法``` `expr $a + $b` ```结果为30 
   
   ② -：减法``` `expr $a - $b` ```结果为-10
   
   ③ *：乘法``` `expr $a \* $b` ```结果为200
  
   ④ / ：除法``` `expr $b/$a` ``` 结果为2

  2）算数运算2
  
  a=10 b=20
  
  ① % ：取余 ``` `expr $a % $b` ```结果为10
  
  ② = ：赋值 a=$b 将把变量b的值赋给a
  
  ③ ==：相等 相同则返回true：[ $a == $b ]返回true
  
  ④ - ！=：不相等 不相同则返回true：[ $a != $b ]返回true
  

  3)算数运算3
  
   ① -eq  检测相等[ $a -eq $b ] 返回false
   
   ② -ne  检测不相等 [ $a -ne $b] 返回true
   
   ③  -gt   检测左边是否大于右边 [ $a -gt $b] 返回false
   
   ④ -lt    检测左边是否小于右边 [ $a -lt $b ] 返回true
   
   ⑥ -ge  检测左边是否大于等于右边 [ $a -ge $b ] 返回false
   
   ⑦ -le    检测左边是否大于等于右边 [ $a -le $b ] 返回true

  ## 3.bash与目录命令
  
   1）创建目录并生成文件
 ```
  mkdir  test
  cd test
  echo “hello”>test.txt
  ls
```      
2）bash 与内存

          统计内存使用：
          for i in `ps aux | awk '{print $6}' |grep -v 'RSS'`
                  count=$[$count+$i]
          echo  "$count/kb"

   实战1：
   ```
   #!/bin/bash
   echo $1,$2,$3
   echo "文件名" $0
   echo "参数数量" $#
   echo "all "$*
   echo "return " $|?
   ```

实战2：
```
#!/bin/bash
a=10
b=20
echo `expr $a + $b`
echo `expr $a - $b`
echo `expr $a \* $b`
echo `expr $a / $b`
echo `expr $a % $b`
```

实战3：
```
#!/bin/bash
mkdir test
cd test
echo "hello" > test.txt
cat test.txt 
```
