
1.查找文件 是否修改
---------------------------------------------------
md5sum

find  ***文件  -type f -exec md5sum {} \;  >  **文件
---------------------------------------------------



2 .修改开启启动项
     bachrc /单个用户

  /etc/rc.local  // 

 1 cat /etc/rc.local  
 2 grep -v "^$"   /文件/file  -n      // 过滤空格  -n 显示行号
 
3 开启启动服务
   /etc/init.d/   下面都是服务器脚本
   
  $> 输出
  
  /etc/passwd  // 所有用户
  
  1-------
  rmp 校验文件
  rpm -V  文件
  
  S 文件大小
  5 MD5 
  T 修改时间
  D 主从设备不
  G  用户组
  U  用户
  
  rmp -v > rpm_check.txt  //建议
  2------------
  find  文件夹  -mtime -2 
  查找最近被修改的文件
  
---------------------------------------------------
修改命令


// which find   --查找命令

cp /bin/find   /bind /ffind

rm -rf /bin/find


chmod +x //加权限

----------------------------