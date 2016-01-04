

1 ifconfig


  ifconfig | grep broadast  //筛选
  
  ifconfig | grep broadcast | awk '{ print $2}'
  
  -- 修改ip
     nmtui -edit
     
     system restart network --重启网络
      
 // 脚本
 
  1  vim ip.sh
   
    bin/bash // 执行环境
   
    ipaddress = ifconfig | grep broadcast | awk '{ print $2}'
    echo ipaddress
   
     sh ip.sh // 运行脚本
    
   2  awk 分隔符 空格 ，可以用-F
     
     cat /etc/passwd | awk -F : '$3 >1000 {print $3 "\t" $7 }'
     cat /etc/passwd | awk -F : '$3 >1000 && $7=="/bin/bash" {print $3 "\t" $7 }'
     cat /etc/passwd | awk -F : '$3 >1000 {print $3 "\t" $7 }' |grep bash
   
   3 begin end 特殊字符
   
     cat /etc/passwd | awk -F : 'BEGIN {print 'name \t shell'}' '$3 >1000 && $7=="/bin/bash" {print $3 "\t" $7 }'
     
     
     
     cat /etc/passwd | awk -F : 'BEGIN {print 'name \t shell'}' '$3 >1000 && $7=="/bin/bash" {print $3 "\t" $7 }'
     
     
   4 删除指令 脚本
   
     vi  userDel.sh
      
      #!/bin/bash
      
      user =cat /etc/passwd | awk -F : '$3 >1000 && $7=="/bin/bash" {print $3 "\t" $7 }'
      
      for i in $user
      do
          userdel -r $i
          
      chmod u+x userDel.sh //分配权限
      
      ls /home/
      
      ./userdel.sh 
      
     ***
     
     5  free -m 系统内容 
            #!/bin/bash
            echo "此脚本可以用来查看当前内存使用百分比"
            use=$(free -m | grep "Mem:" | awk '{print $3}')            
            total=$(free -m | grep "Mem:" | awk '{print $2}')
            useper=$(expr $use \* 100 / $total)
            echo "系统当前内存使用百分比为:"
            echo ${useper}%

      
       
      
      
     
      
   
    