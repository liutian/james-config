james-config
============
## 系统依赖环境：
1.jdk1.5或1.6,但不能是1.7否则读取xml文件时会报错  
2.因为james用到了1024以下的端口，所以必须用root用户进行操作  
3.linux系统必须安装libc6软件包不同linux系统下该软件包名字不同，需要上网查询对于的安装包的名称 
4.james默认监听25,110,143等端口，请确保这些端口未被占用，查看端口占用命令为:`lsof -i:25`  
#### 注意在邮件服务器上发邮件给本邮件服务器时程序的smtp.host:localhost
## 安装与配置
1.下载并解压james软件包  
2.james内置了一套配置，如果想自定义配置，则使用conf/中james已经提供的配置文件模板进行自定义，最后记得将XXX-temple.properties文件名改为XXX.properties  
3.自定义配置：  
### james-database-template  数据库配置,已mysql为例  
  database.driverClassName=com.mysql.jdbc.Driver  
  database.url=jdbc:mysql://10.253.53.22:3306/mailserver?zeroDateTimeBehavior=convertToNull&autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;create=true  
  database.username=root  
  database.password=slothdb123  
  vendorAdapter.database=MYSQL  
  注意：需要将对应的数据库驱动包拷贝到conf/lib/下，如果报错找不到数据库驱动包时需要修改wrapper.conf文件：
  `wrapper.java.classpath.120=../conf/lib/mysql-connector-java-5.0.8-bin.jar`添加这一行，运行bin/run.bat或bin/james.bat将会自动建立起数据库表结构 
### domainlist-template.conf 邮件服务器域名配置  
`<domainlist class=org.apache.james.domainlist.xml.XMLDomainList>`  
`<domainnames> `   
` <domainname>findest.com.cn</domainname>  `  
`</domainnames>  `  
`<autodetect>false</autodetect>  `  
`<autodetectIP>false</autodetectIP>  `  
`<defaultDomain>findest.com.cn</defaultDomain> `   
`</domainlist>`  
注释掉`<domainlist class="org.apache.james.domainlist.jpa.JPADomainList"> ... </domainlist>`  
### dnsservice-template.conf 配置邮件服务器dns
`<servers>`  
`<server>61.177.7.1</server>`  
`<server>...</server>`  
`</servers>`  
### usersrepository-template.conf 修改用户存储方式
注释掉：  
`<usersrepository name="LocalUsers" class="org.apache.james.user.jpa.JPAUsersRepository">`  
    `<algorithm>MD5</algorithm>`  
    `<enableVirtualHosting>false</enableVirtualHosting>`  
`</usersrepository>`    
启用:  
`<usersrepository name="LocalUsers" class="org.apache.james.user.jdbc.JamesUsersJdbcRepository" destinationURL="db://maildb/users">`  
    `<sqlFile>file://conf/sqlResources.xml</sqlFile>`  
    `<ignoreCase>true</ignoreCase>`  
    `<enableAliases>true</enableAliases>`  
    `<enableForwarding>true</enableForwarding>`  
    `<enableVirtualHosting>true</enableVirtualHosting>`    
`</usersrepository>`  
### smtpserver-template.conf  
启用`<authRequired>true</authRequired>`邮件服务器之外的机子通过该邮件服务器发邮件时必须验证密码，邮件服务器所在的程序发邮件给该邮件服务器时会忽略密码验证  
修改`<helloName autodetect="false">findest.com.cn</helloName>`  

  
  
    
