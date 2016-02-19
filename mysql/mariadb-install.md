mySql =》 mariaDb 
1.检查是否安装

            rpm -qa | grep mariadb
            
            rpm -e --nodeps mariadb-* 删除命令
        
2.安装 

            yum -y install mariadb*
        
     
3.服务操作

            systemctl start mariadb  #启动MariaDB
            systemctl stop mariadb  #停止MariaDB
            systemctl restart mariadb  #重启MariaDB
            systemctl enable mariadb  #设置开机启动
    
4. 创建登录用户 [use mysql] 数据库操作 *

            mysql -uroot -p  //回车直接登陆
       
            命令:CREATE USER 'username'@'host' IDENTIFIED BY 'password'; 
            说明:username - 你将创建的用户名, host - 指定该用户在哪个主机上可以登陆,
            如果是本地用户可用localhost, 如果想让该用户可以从任意远程主机登陆,可以使用通配符%.
             password - 该用户的登陆密码,密码可以为空,如果为空则该用户可以不需要密码登陆服务器. 
             
             eg.
             CREATE USER 'pig'@'192.168.1.101_' IDENDIFIED BY '123456'; 
             CREATE USER 'pig'@'%' IDENTIFIED BY '123456'; 
             
             --- CREATE USER 'mango'@'%' IDENTIFIED BY 'feieidemao'
               
 5.授权
            
            命令:GRANT privileges ON databasename.tablename TO 'username'@'host' 
            说明: privileges - 用户的操作权限,如SELECT , INSERT , UPDATE 等(详细列表见该文最后面).
            如果要授予所的权限则使用ALL.;databasename - 数据库名,tablename-表名,
            如果要授予该用户对所有数据库和表的相应操作权限则可用*表示, 如*.*. 
            
            eg.
             GRANT SELECT, INSERT ON test.user TO 'pig'@'%'; 
             GRANT ALL ON *.* TO 'pig'@'%';
             
             --  GRANT ALL ON *.* TO 'mango'@'%';
             --  GRANT ALL PRIVILEGES ON *.* TO 'mango'@'%'IDENTIFIED BY 'feieidemao' WITH GRANT OPTION;
 6.设置与更改用户密码
             
            命令:
            SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');如果是当前登陆用户用SET PASSWORD = PASSWORD("newpassword"); 
            
            例子: SET PASSWORD FOR 'pig'@'%' = PASSWORD("123456"); 
 7.撤销用户权限
       
            命令: REVOKE privilege ON databasename.tablename FROM 'username'@'host'; 
            
            说明: privilege, databasename, tablename - 同授权部分. 
            
            例子: REVOKE SELECT ON *.* FROM 'pig'@'%'; 
            
            注意: 假如你在给用户'pig'@'%'授权的时候是这样的(或类似的):GRANT SELECT ON test.user TO 'pig'@'%', 则在使用REVOKE SELECT ON *.* FROM 'pig'@'%';命令并不能撤销该用户对test数据库中user表的SELECT 操作.相反,如果授权使用的是GRANT SELECT ON *.* TO 'pig'@'%';则REVOKE SELECT ON test.user FROM 'pig'@'%';命令也不能撤销该用户对test数据库中user表的Select 权限. 
            
            具体信息可以用命令SHOW GRANTS FOR 'pig'@'%'; 查看. 
            
 8.MySQL安全配置向导mysql_secure_installation详解
 
           [root@server1 ~]# mysql_secure_installation
           NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MySQL
           SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!
           In order to log into MySQL to secure it, we'll need the current
           password for the root user. If you've just installed MySQL, and
           you haven't set the root password yet, the password will be blank,
           so you should just press enter here.
           Enter current password for root (enter for none):<–初次运行直接回车
           OK, successfully used password, moving on…
           Setting the root password ensures that nobody can log into the MySQL
           root user without the proper authorisation.
           Set root password? [Y/n] <– 是否设置root用户密码，输入y并回车或直接回车
           New password: <– 设置root用户的密码
           Re-enter new password: <– 再输入一次你设置的密码
           Password updated successfully!
           Reloading privilege tables..
           … Success!
           By default, a MySQL installation has an anonymous user, allowing anyone
           to log into MySQL without having to have a user account created for
           them. This is intended only for testing, and to make the installation
           go a bit smoother. You should remove them before moving into a
           production environment.
           Remove anonymous users? [Y/n] <– 是否删除匿名用户,生产环境建议删除，所以直接回车
           … Success!
           Normally, root should only be allowed to connect from 'localhost'. This
           ensures that someone cannot guess at the root password from the network.
           Disallow root login remotely? [Y/n] <–是否禁止root远程登录,根据自己的需求选择Y/n并回车,建议禁止
           … Success!
           By default, MySQL comes with a database named 'test' that anyone can
           access. This is also intended only for testing, and should be removed
           before moving into a production environment.
           Remove test database and access to it? [Y/n] <– 是否删除test数据库,直接回车
           - Dropping test database…
           … Success!
           - Removing privileges on test database…
           … Success!
           Reloading the privilege tables will ensure that all changes made so far
           will take effect immediately.
           Reload privilege tables now? [Y/n] <– 是否重新加载权限表，直接回车
           … Success!
           Cleaning up…
           All done! If you've completed all of the above steps, your MySQL
           installation should now be secure.
           Thanks for using MySQL!
           [root@server1 ~]#
 
            
 