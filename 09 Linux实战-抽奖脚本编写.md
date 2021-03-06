# 九、Linux实战-抽奖脚本编写
1.前提：已创建有名单的文件 

例如：tmp.txt 文件

2.解题思路：

1）首先，读取名单文件
```
#!/bin/bash
seeds=`while read line;do echo $line;done < tmp.txt`
echo $seeds
```
结果：读取文件之后，发现有的人员名称中有空格，需要将空格替换为“..”

 2)替换人员姓名中的空格
 ```
 #!/bin/bash
 seeds=`while read line;do echo ${line// /..};done < tmp.txt`
 echo $seeds
```
  此处也可以使用sed处理。
  
3)将脚本放置函数中：
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
}
rand
```
bash语言中默认所有变量为全局变量，加local之后变更为局部变量。

4）从seeds中筛选出一部分人
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
  while [[$count != 1 ]];do
    seeds=`for i in $seeds;do (($RANDOM%2)) && echo $i;done`
    count=`echo "seeds" | wc -l`
  done
  echo $seeds
}

rand
```
RANDOM 是一个随机数，任何一个数字对2取余之后只有1或0 的结果。
当结果为0 时，&& 的结果为空，不进行打印；当为1时进行打印。

结果：运行之后会出现一个bug，会有一定的几率全部不打印，结果为空。

5）需增加去掉空白脚本：
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
  while [[$count != 1 ]];do
    seeds=`for i in $seeds;do (($RANDOM%2)) && echo $i;done`
    count=`echo "seeds" | wc -l`
  done
  if [[ $seeds == ""]];then
   rand
  else 
  echo $seeds
  fi
}

rand
```

6)执行该脚本20次：
`for ((i=0;i<20;i++));do bash lottery.sh ; done`

7)增加实现筛选出多个人：
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
  while [[$count != 1 ]];do
    seeds=`for i in $seeds;do (($RANDOM%2)) && echo $i;done`
    count=`echo "seeds" | wc -l`
  done
  if [[ $seeds == ""]];then
   rand
  else 
  echo $seeds
  fi
}
res(){
    for A in {1..10};do
    tmp=`rand`
    arrs[$A]=$tmp
    done
    echo ${arrs[@]}
}
res
rand
```
注：打印数组所有内容：arrs[@]

8）实现去重：
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
  while [[$count != 1 ]];do
    seeds=`for i in $seeds;do (($RANDOM%2)) && echo $i;done`
    count=`echo "seeds" | wc -l`
  done
  if [[ $seeds == ""]];then
   rand
  else 
  echo $seeds
  fi
}
res(){
    for A in {1..10};do
    tmp=`rand`
    while [[`is_repeat $tmp` == 0]];do
       tmp=rand
    done   
    arrs[$A]=$tmp
    done
    echo ${arrs[@]}
}
is_repeat(){
    for arr in ${arrs[@]};do
     if [[$arr == $1]];then
      echo 0;
      return 0;
     fi 
    done
    echo 1;
}
res
rand
```

9）增加实现从脚本外面传参数到脚本中，来筛选个数：
```
#!/bin/bash
rand(){
  local seeds=`while read line;do echo ${line// /..} ;done < tmp.txt`    
  local count=0
  while [[$count != 1 ]];do
    seeds=`for i in $seeds;do (($RANDOM%2)) && echo $i;done`
    count=`echo "seeds" | wc -l`
  done
  if [[ $seeds == ""]];then
   rand
  else 
  echo $seeds
  fi
}
res(){
    for A in ((A=0;A<$1;A++));do
    tmp=`rand`
    while [[`is_repeat $tmp` == 0]];do
       tmp=rand
    done   
    arrs[$A]=$tmp
    done
    echo ${arrs[@]}
}
is_repeat(){
    for arr in ${arrs[@]};do
     if [[$arr == $1]];then
      echo 0;
      return 0;
     fi 
    done
    echo 1;
}
res $1
rand
```

最终脚本：
```
#!/bin/bash
#筛选出一个人
rand(){
 #从文件中读取所有人的信息，用..代替空格  
 local seeds=`while read line;do echo ${line// /..};done<tmp.txt`
 local conut=0
 #不停地进行筛选，直到只剩一个同学为止
   while [[$count != 1 ]];do
      #从seeds 中筛选出一部分人进行猜拳操作，如果是1，进行下一轮，如果是0，则淘汰
     seeds=`for i in seeds;do ((RABNDOM%2)) && echo $i;done`
     #计算当前幸运人数
     count=`echo "seeds | wc -l "`
   done
   #如果发现是空，就再进行筛选
   if [[$seeds == ""]];then
      #递归调用，本函数
      rand
   else 
      echo $seeds   
   fi   
}
#筛选出多个人
res(){
    #此处$1是别人传给res的值
    for((A=0;A<$1;A++));do
    tmp=`rand`
    #去重
      while [[`is_repeat $tmp` == 0]];do
        tmp=`rand`
      done
    arrs[$A]=$tmp
    done
    #打印数组所有内容
    echo ${arrs[@]}
}
#去重函数定义
#把输进来的数据与组内的值进行比较
#如果有相同的值，则echo=0
#如果没有相同的值，则echo=1
is_repeat(){
    #遍历数组
    for arr in $arrs{[@]};do
       #把输进来的值与每一个值进行比较
       if [[$arr == $1]];then
         #如果相同，输出0
         echo 0;
         return 0;
       fi  
    done
    #如果没有相同值，则输出1
    echo 1
}
#此处$1 是传的参数的第一个值
res $1
rand
```

