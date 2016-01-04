kvm 虚拟化

优点： 1.把分散的资源整合一块，统一管理
      2.
      
产品
    vmware
    kvm  rhel6_x64
    xen[kernel-xen]
    
    
    openstack 云计算
    
    
 kvm 内核虚拟化 ,免费 ，硬件辅助虚拟化
 
 kvm 不能在32位上添加
 实战：部署kvm 虚拟化
   
    1 cup 是否支持虚拟化 
  
    cat /proc/cuinfo | grep --color vmx
    
    2 
    
    3 mkfs.ext4 /dev/sdb1  格式化
    
    
    安装kvm 
    
      1 安装模块 ，管理工具 和  libvirt服务，命令安装
      
      2
      
      service libvirtd start
      
      chkconfig li
      
      
      1// lsmod | grep kvm 查看是否安装
      
      
      mount  /var 
