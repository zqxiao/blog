[TOC]

# 1. 压缩

``` sh

#解压

tar zxvf 文件名.tar.gz

#压缩

 tar zcvf 文件名.tar.gz 目标名

```



# 2. 远程文件复制

通过ssh拷贝文件   

``` sh 

＃scp  用户名@ip:/远程目录(文件)  /本地文件(目录)

scp  oracle@172.20.1.61:/home/oracle/db_bk/xxx.dmp /u01/

```

     

# 3. 查找

``` sh

find .|xargs grep -ri "重复出库了"     

```

                                                             

＃ 4. 在文件中查找    

``` sh

grep -w  'JIS物料拉动单begin' trace-all.log     

grep -w  'JIS物料拉动单begin' *.log     

#如果想搜以特定字符开头（结尾）的单词，可以这样：    

grep  '\<seven' test.txt    

grep  'seven\>' test.txt    

#如果想搜以特定字符开头（结尾）的行，可以这样：    

grep  '^seven' test.txt    

grep  'seven$' test.txt    

#想要显示目标行的上下文    

grep  -C 1 'JIS物料拉动单begin' trace-all.log    

#到底是显示上文还是下文？    

 grep -A 1 'JIS物料拉动单begin' trace-all.log     

 grep -B 1 'JIS物料拉动单begin' trace-all.log     

#查找多个    

grep  -E "(six|seven|eight)" test.txt    

```

                        

# 5. Linux如何根据进程名称的一部分kill掉进程    

``` sh

ps -ef |  grep javadeploy.jar | grep -v grep | awk '{print $2}' | xargs  --no-run-if-empty kill    

```

# 6. 统计网络状态

``` sh



netstat -n |awk '/^tcp/{++S[$NF]}END{for (i in S ) print i,S[i]}'

TIME_WAIT 138

ESTABLISHED 9

``` 



                       

# 7. vim查找     

查找    :/target    查找下一个n    查找上一个N    

重新加载    :e!    



# 8. yum

>系统添加删除软件是常事，yum同样可以胜任这一任务，只要软件是rpm安装的。
安装的命令是，yum install xxx，yum会查询数据库，有无这一软件包，如果有，则检查其依赖冲突关系，如果没有依赖冲突，那么最好，下载安装;如果有，则会给出提示，询问是否要同时安装依赖，或删除冲突的包，你可以自己作出判断。
删除的命令是，yum remove xxx，同安装一样，yum也会查询数据库，给出解决依赖关系的提示。

方法/步骤



``` sh 

#用YUM安装软件包
yum install <package_name>

#用YUM删除软件包
yum remove <package_name>

```



# 9. 性能测试

``` sh 

ab -c 50 -n 10000 http://10.36.8.44:10311/kanban/carousel

This is ApacheBench, Version 2.3 <$Revision: 1706008 $>

Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/

Licensed to The Apache Software Foundation, http://www.apache.org/



Benchmarking 10.36.8.44 (be patient)

Completed 100 requests

Completed 200 requests

Completed 300 requests

Completed 400 requests

Completed 500 requests

Completed 600 requests

Completed 700 requests

Completed 800 requests

Completed 900 requests

Completed 1000 requests

Finished 1000 requests





Server Software:        thin

Server Hostname:        10.36.8.44

Server Port:            10311



Document Path:          /kanban/carousel

Document Length:        12223 bytes



Concurrency Level:      20

Time taken for tests:   86.903 seconds

Complete requests:      1000

Failed requests:        0

Total transferred:      12940000 bytes

HTML transferred:       12223000 bytes

Requests per second:    11.51 [#/sec] (mean)

Time per request:       1738.069 [ms] (mean)

Time per request:       86.903 [ms] (mean, across all concurrent requests)

Transfer rate:          145.41 [Kbytes/sec] received



Connection Times (ms)

              min  mean[+/-sd] median   max

Connect:        2  186 272.3     96    1714

Processing:    76 1547 1514.3   1175   13117

Waiting:       75 1265 1246.2    986   11935

Total:        279 1733 1528.3   1359   13348



Percentage of the requests served within a certain time (ms)

  50%   1359

  66%   1643

  75%   1962

  80%   2265

  90%   2754

  95%   3997

  98%  10321

  99%  10344

 100%  13348 (longest request)

```





# 10. 端口转发

``` shell

ssh -f root@10.36.8.88 -L 127.0.0.1:11521:172.22.0.10:1521 -N

```



# 11. xml 转java类

三步： xml --> xsd --> java

xml --> xsd 使用在线工具

 http://www.freeformatter.com/xsd-generator.html#ad-output

xsd --> java 使用xjc命令（xjc －p 包名，-d ./ java文件输出在当前路径下， 最后一个参数就是xsd的路径）

xjc -d ./ -p com.ewin.mes.intf.dataobject  esb.xsd



# 12. find 和mv 结合使用

``` shell 

＃ find . -name "trace-all.log.[1-9][0-9][0-9]" | xargs -I '{}' mv {} ../hessian_bak_20160616/

``` 

使用-i参数默认的前面输出用{}代替，-I参数可以指定其他代替字符。



# 13. 烧制USB启动盘

挂载盘列表

diskutil list

弹出/dev/disk3

diskutil unmountDisk /dev/disk3

烧制

sudo dd if=~/Downloads/CentOS-6.8-x86_64-LiveDVD/CentOS-6.8-x86_64-LiveDVD.dmg  of=/dev/disk3 bs=1m





# 14. linux下tar命令



tar zxvf /bbs.tar.zip -C /zzz/bbs    

//把根目录下的bbs.tar.zip解压到/zzz/bbs下，前提要保证存在/zzz/bbs这个目录 

这个和cp命令有点不同，cp命令如果不存在这个目录就会自动创建这个目录！



附：用tar命令打包

例：将当前目录下的zzz文件打包到根目录下并命名为zzz.tar.gz

tar zcvf /zzz.tar.gz ./zzz



``` 

tar

-c: 建立压缩档案
-x：解压
-t：查看内容
-r：向压缩归档文件末尾追加文件
-u：更新原压缩包中的文件

这五个是独立的命令，压缩解压都要用到其中一个，可以和别的命令连用但只能用其中一个。下面的参数是根据需要在压缩或解压档案时可选的。

-z：有gzip属性的
-j：有bz2属性的
-Z：有compress属性的
-v：显示所有过程
-O：将文件解开到标准输出

下面的参数-f是必须的

-f: 使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名。

# tar -cf all.tar *.jpg
这条命令是将所有.jpg的文件打成一个名为all.tar的包。-c是表示产生新的包，-f指定包的文件名。

# tar -rf all.tar *.gif
这条命令是将所有.gif的文件增加到all.tar的包里面去。-r是表示增加文件的意思。

# tar -uf all.tar logo.gif
这条命令是更新原来tar包all.tar中logo.gif文件，-u是表示更新文件的意思。

# tar -tf all.tar
这条命令是列出all.tar包中所有文件，-t是列出文件的意思

# tar -xf all.tar
这条命令是解出all.tar包中所有文件，-x是解开的意思

```





# 15. linux下mysql数据导入导出

```


将113的数据库（93）导入到112数据库(115)
登陆到93
#mysqldump -h10.0.14.93 -umdm -pmdm mdm>/tmp/mdm_bak.sql
压缩
#cd /tmp
#tar -zcvf mdm_bak.tar.gz /tmp/mdm_bak.sql

将压缩文件导入到115上的  /tmp/ 目录下
// ＃scp  root@10.0.14.93:/tmp/mdm_bak.tar.gz  /tmp
登陆到115
解压
#tar -zxvf /tmp/mdm_bak.tar.gz
#mysql -umdm -pmdm -h10.0.15.151 mdm</tmp/mdm_bak.sql
```



# 16. 查看端口占用

```

mac :   lsof -i:8080

Linux : neststat -anltp | grep 8080

```