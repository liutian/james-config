james-config
============
## 系统依赖环境：
1.jdk1.5或1.6,但不能是1.7否则读取xml文件时会报错  
2.因为james用到了1024以下的端口，所以必须用root用户进行操作  
3.linux系统必须安装libc6软件包不同linux系统下该软件包名字不同，需要上网查询对于的安装包的名称 
4.james默认监听25,110,143等端口，请确保这些端口未被占用，查看端口占用命令为:`lsof -i:25`  
## 安装与配置
1.下载并解压james软件包  
2.james内置了一套配置，如果想自定义配置，则使用conf/中james已经提供的配置文件模板进行自定义，最后记得将XXX-temple.properties文件名改为XXX.properties  
3.自定义配置：  
### james-database-template  数据库配置,已mysql为例  
  database.driverClassName=com.mysql.jdbc.Driver  
  database.url=jdbc:mysql://10.253.53.22:3306/mailserver?zeroDateTimeBehavior=convertToNull&autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=UTF-8  
  database.username=root  
  database.password=slothdb123  
  vendorAdapter.database=MYSQL  
  注意：需要将对应的数据库驱动包拷贝到conf/lib/下，运行bin/run.bat将会自动建立起数据库表结构 
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
### wrapper.conf
添加`wrapper.java.classpath.120=../conf/lib/mysql-connector-java-5.0.8-bin.jar`,记得将数据库驱动拷贝到conf/lib下

  
  
    
