# 01-Linux基本用法
## 一、Linux基本使用方法
### 1.常用的shell：
- Bourne Shell（/user/bin/sh或/bin/sh）
- Bourne Again Shell (/bin/bash)
- C Shell (/user/bin/csh)
- K Shell (/user/bin/ksh)
- Shell for Root(/sbin/sh)
### 2. bash 示例：
  ```bash
    #!/bin/bash'
    echo "hello!" 
  ```

执行该文件：chmod +x ./tesh.sh
./test.sh  执行脚本

或：
   /bin/sh test.sh  
   指定了Bourne shell 
   执行（与Bourne Again shell 区别很小）
   
### 3.实战演练：
- ls：查看文件目录
- rm -rf  test.sh :删除test.sh文件
- vim test.sh:新建test.sh文件的同时进行编辑
    ```
   #！/bin/bash
    echo "hello!"
    
     :wq(保存加退出)
   ```
        
- cat test.sh: 查看test文件的内容
- ./test.sh :执行该文件#
- chmod +x test.sh:修改test文件的权限，增加可执行的权限
- /bin/sh test.sh :执行该文件

# 笔记链接

- [02 Linux的常用命令](https://github.com/tete1987/01-Linux/blob/master/02%20Linux%E7%9A%84%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4.md)

- [03 Linux三剑客与管道使用](https://github.com/tete1987/01-Linux/blob/master/03%20Linux%E4%B8%89%E5%89%91%E5%AE%A2%E4%B8%8E%E7%AE%A1%E9%81%93%E4%BD%BF%E7%94%A8.md)
- [04 Bash编程语法](https://github.com/tete1987/01-Linux/blob/master/04%20Bash%E7%BC%96%E7%A8%8B%E8%AF%AD%E6%B3%95.md)

- [05 Bash基本使用](https://github.com/tete1987/01-Linux/blob/master/05%20Bash%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8.md)

- [06 Linux进阶命令](https://github.com/tete1987/01-Linux/blob/master/06%20Linux%E8%BF%9B%E9%98%B6%E5%91%BD%E4%BB%A4.md)

- [08 Linux三剑客实战](https://github.com/tete1987/01-Linux/blob/master/08%20Linux%E4%B8%89%E5%89%91%E5%AE%A2%E5%AE%9E%E6%88%98.md)

- [09 Linux实战-抽奖脚本编写](https://github.com/tete1987/01-Linux/blob/master/09%20Linux%E5%AE%9E%E6%88%98-%E6%8A%BD%E5%A5%96%E8%84%9A%E6%9C%AC%E7%BC%96%E5%86%99.md)

- [10 Linux之性能命令](https://github.com/tete1987/01-Linux/blob/master/10%20Linux%E4%B9%8B%E6%80%A7%E8%83%BD%E5%91%BD%E4%BB%A4.md)
