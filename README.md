james-config
============
## 系统依赖环境：
1.jdk1.5或1.6,但不能是1.7否则读取xml文件时会报错  
2.必须用root用户进行操作  
3.linux系统必须安装libc6软件包不同linux系统下该软件包名字不同，需要上网查询对于的安装包的名称    
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
  
  
    
