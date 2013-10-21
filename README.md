james-config
============
## 系统依赖环境：
1.jdk1.5或1.6,但不能是1.7否则读取xml文件时会报错  
2.必须用root用户进行操作  
3.必须按照libc6软件包 ，不同linux系统下该软件包名字不同，需要特别注意  
## 安装配置
1.下载并解压架包  
2.首先配置文件夹中的配置文件：
  ### james-database-template  数据库配置,已mysql为例  
    
  database.driverClassName=com.mysql.jdbc.Driver  
  database.url=jdbc:mysql://10.253.53.22:3306/mailserver?zeroDateTimeBehavior=convertToNull&autoReconnect=true&amp;useUnicode=true&amp;characterEncoding=UTF-8  
  database.username=root  
  database.password=slothdb123  
  vendorAdapter.database=MYSQL  
  注意：需要将对于的数据库驱动架包拷贝到conf/lib/下  
    
  ### 
