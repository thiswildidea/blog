---
layout: pos
title: ArcGIS Enterprise install for linux standalone
date: 2020-07-13 14:16:49
categories:
- ArcGIS-Enterprise
tags:
- arcgis
- install
- linux
---
本文以 Redhat7.4 上安装 ArcGIS Enterprise 10.7 为例详细阐述了单机环境下
ArcGIS Enterprise 的完整安装。
# 目录
 - [准备](#准备)
   - [防火墙的关闭](#防火墙的关闭)
   - [用户和组的创建](#用户和组的创建)
   - [IP和机器名](#IP和机器名)
     - [编辑/etc/hostname](#编辑/etc/hostname)
     - [编辑/etc/hosts](#编辑/etc/hosts)
     - [主机名检测](#主机名检测)
   - [准备安装包](#准备安装包)
     - [拷贝安装包至/home/arcgis下](#拷贝安装包至/home/arcgis下)
     - [解压](#解压)
     - [修改权限](#修改权限)
 - [安装和配置ArcGISforServer](#安装和配置ArcGISforServer)
   - [安装前准备](#安装前准备)
     - [编辑limits.conf文件](#编辑limits.conf文件)
     - [诊断当前环境是否满足Server安装要求](#诊断当前环境是否满足Server安装要求)
   - [安装ArcGISforServer](#安装ArcGISforServer)
   - [配置ArcGISforServer](#配置ArcGISforServer)
 - [安装和配置ArcGISDataStore](#安装和配置ArcGISDataStore)
   - [安装前准备](#安装前准备)
     - [设置vm.swappiness](#设置vm.swappiness)
     - [诊断当前环境是否满足DataStore安装要求](#诊断当前环境是否满足DataStore安装要求)
   - [安装ArcGISDataStore](#安装ArcGISDataStore)
   - [配置ArcGISDataStore](#配置ArcGISDataStore)
 - [安装和配置PortalforArcGIS](#安装和配置PortalforArcGIS)
   - [安装前准备](#安装前准备)
     - [诊断当前环境是否满足PortalforArcGIS安装要求](#诊断当前环境是否满足PortalforArcGIS安装要求)
   - [安装PortalforArcGIS](#安装PortalforArcGIS)
   - [配置PortalforArcGIS](#配置PortalforArcGIS)
 - [安装和配置WebAdaptor](#安装和配置WebAdaptor)
   - [安装前准备](#安装前准备)
     - [安装JDK](#安装JDK)
       - [解压JDK](#解压JDK)
       - [配置JDK环境变量](# 配置JDK环境变量)
     - [安装tomcat](#安装tomcat)
       - [解压tomcat](#解压tomcat)
       - [创建自签名证书](#创建自签名证书)
       - [对tomcat启用ssl](#对tomcat启用ssl)
       - [启动和验证tomcat](#启动和验证tomcat)
   - [安装和部署 Web Adaptor](#安装和部署WebAdaptor)
       - [安装 Web Adaptor](#安装WebAdaptor)
       - [部署WebAdaptor到tomcat下](#部署WebAdaptor到tomcat下)
   - [配置 Web Adaptor](#配置WebAdaptor)
     - [对 Portal for ArcGIS 配置名为 arcgis 的 Web Adaptor](#对PortalforArcGIS配置名为arcgis的WebAdaptor)
     - [对 ArcGIS for Server 配置名为 server 的 Web Adaptor](#对ArcGISforServer配置名为server的WebAdaptor)
 - [实现 Portal 和 Server 的托管](#实现Portal和Server的托管)
 - [补充](#补充)
   - [对 ArcGIS for Server 更新证书](#对ArcGISforServer更新证书)
   - [对 Portal for ArcGIS 更新证书](#对PortalforArcGIS更新证书)
   - [在客户端机器上安装证书](#在客户端机器上安装证书)
## 准备
### 防火墙的关闭
停止防火墙
```bash
 [root@gis home]# systemctl stop firewalld.service
```
禁用防火墙的开机启动
```bash
[root@gis home]# systemctl disable firewalld.service
```
查看防火墙状态
```bash
[root@gis home]# systemctl status firewalld.service
```
注意：
```bash
 单机环境下部署 ArcGIS Enterprise 时，可考虑仅开启 (1)80 和 443，确保外部客户端可
通过 web adaptor 访问到 Portal for ArcGIS 或 ArcGIS for Server 服务页面；(2)当 Web
Adaptor 层未启用 ArcGIS for Server 的管理功能时，则需开启 6080 和 6443 端口，确保
外部客户端上的 ArcMap 向此环境下的 ArcGIS for Server 发布服务。关于 ArcGIS
Enterprise 更多的端口信息，请参考下面的链接。
1. ArcGIS Server 所用端口号： 
http://server.arcgis.com/en/server/latest/install/windows/ports-used-by-arcgisserver.htm
2. Portal for ArcGIS 所用端口号：
http://server.arcgis.com/en/portal/latest/administer/windows/ports-used-by-portalfor-arcgis.htm
3. ArcGIS Data Store 所用端口号：
http://server.arcgis.com/en/portal/latest/administer/windows/ports-used-by-arcgisdata-store.htm
```
### 用户和组的创建
[root@gis home]# groupadd shsmi
[root@gis home]# useradd -g shsmi -m arcgis
[root@gis home]# passwd arcgis
### IP和机器名
ArcGIS Enterprise 的安装要求计算机名是完全限定域名的形式。这一修改可通过编辑
/etc/hostname 和/etc/hosts 两个文件实现。
#### 编辑/etc/hostname
```bash
[root@gis ~]# vi /etc/hostname
```
文件内容如下：
agsenterprise
注意： 主机名的设置也可通过运行 `hostnamectl set-hostname agsenterprise` 来实现。
#### 编辑/etc/hosts
```bash
[root@gis ~]# vi /etc/hosts
```
文件内容如下：
127.0.0.1 localhost localhost.localdomain localhost4 localhost4.localdomain4::1 localhost localhost.localdomain localhost6 localhost6localdomain6
192.168.107.195 agsenterprise.shsmi.com agsenterprise
`注意： 多网卡的环境下，建议删除 localhost 所在行`
#### 主机名检测
运行 `hostname` 和 `hostname -f` 进行主机名规范的检测。
```bash
[root@agsenterprise home]# hostname
agsenterprise
```
```bash
[root@agsenterprise home]# hostname -f
agsenterprise.shsmi.com
```
如上所示，主机名和完全限定域名显示无误，符合规范。
### 准备安装包
#### 拷贝安装包至/home/arcgis下
将 ArcGIS_Server_Linux_105_154052.tar.gz、ArcGIS_DataStore_Linux_105_154054.tar.gz、Web_Adaptor_Java_Linux_105_154055.tar.gz 
和Portal_for_ArcGIS_Linux_105_154053.tar.gz 拷贝到/home/arcgis 目录下备用。
#### 解压
依次运行 tar -zxvf 对上步骤中四个安装包进行解压
```bash
[root@agsenterprise arcgis]# tar -zxvf ArcGIS_Server_Linux_105_154052.tar.gz
```
#### 修改权限
依次运行 chown 和 chmod 对上步骤解压后的四个文件夹修改权限。
```bash
[root@agsenterprise arcgis]# chown -R arcgis:shsmi ArcGISServer/
[root@agsenterprise arcgis]# chmod -R 755 ArcGISServer/
```
## 安装和配置ArcGISforServer
### 安装前准备
#### 编辑limits.conf文件
编辑/etc/security/limits.conf 文件，添加如下内容：
 arcgis soft nofile 65535
 arcgis hard nofile 65535
 arcgis soft nproc 25059
 arcgis hard nproc 25059
#### 诊断当前环境是否满足Server安装要求
运行 serverdiag 脚本诊断当前环境是否满足 ArcGIS for Server 安装要求。
```bash
[root@agsenterprise arcgis]# su - arcgis
[arcgis@agsenterprise ~]$ ./ArcGISServer/serverdiag/serverdiag
```
当出现如下信息，说明当前环境满足需求，可安装 ArcGIS for Server。
There were 0 failure(s) and 0 warning(s) found:
### 安装ArcGISforServer
这里利用 console 模式进行交互安装。
```bash
[arcgis@agsenterprise ~]$ cd ArcGISServer/
[arcgis@agsenterprise ArcGISServer]$ ./Setup -m console
```
安装完毕，显示如下信息，说明安装成功。
Congratulations. ArcGIS Server 10.7 has been successfully installed to:/home/arcgis/arcgis/server
You will be able to access ArcGIS Server Manager by navigating to
http://agsenterprise.shsmi.com:6080/arcgis/manager
PRESS <ENTER> TO EXIT THE INSTALLER:
### 配置ArcGISforServer
在浏览器中输入上步骤中返回的 ArcGIS Server Manager 地址，自动跳转至 ArcGIS for Server 的 6443 端口，开始进行站点配置。
1 点击创建新站点
![创建新站点](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/createsite.png)
2 设置主站点管理员账户的用户名和密码，点击下一步。
![设置站点用户名和密码](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/createsite1.png)
3 设置根服务器目录和配置存储的位置，点击下一步。
![设置站点用户名和密码](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/createsite2.png)
4 点击完成，直至安装成功。
## 安装和配置ArcGISDataStore
### 安装前准备
#### 设置vm.swappiness
设置 vm.swappiness 和 vm.max_map_count 的值，以满足时空大数据分析的需要
```bash
[root@agsenterprise arcgis]# echo 'vm.max_map_count = 262144' >> /etc/sysctl.conf
[root@agsenterprise arcgis]# echo 'vm.swappiness = 1' >> /etc/sysctl.conf
```
运行如下命令使上述变更生效。
```bash
[root@agsenterprise arcgis]# /sbin/sysctl -p
```
#### 诊断当前环境是否满足DataStore安装要求
运行 datastorediag 脚本诊断当前环境是否满足 ArcGIS DataStore 的安装要求。
```bash
[root@agsenterprise arcgis]# su - arcgis
[arcgis@agsenterprise ~]$ ArcGISDataStore_Linux/datastorediag/datastorediag
```
当出现如下信息，说明当前环境满足需求，可安装 ArcGIS DataStore。
There were 0 failure(s) and 0 warning(s) found:
### 安装ArcGISDataStore
这里利用 silent 模式进行静默安装。
```bash
[arcgis@agsenterprise ~]$ cd ArcGISDataStore_Linux/
[arcgis@agsenterprise ArcGISDataStore_Linux]$ ./Setup -m silent -l
Yes
```
安装完毕，显示如下信息，说明安装成功。
...ArcGIS Data Store 10.7 installation is complete.
You will be able to configure ArcGIS Data Store 10.7 by navigating to https://localhost:2443/arcgis/datastore
### 配置ArcGISDataStore
在浏览器中输入 ArcGIS Data Store 的访问地
址 https://agsenterprise.shsmi.com:2443/arcgis/datastore/ ,开始进行 ArcGIS DataStore 的配置
1.输入上述步骤中的 ArcGIS Server 的地址以及ArcGIS for Server 主站点管理员账户的用户名和密码 ，点击下一步。
 设置内容目录的位置，点击下一步。
 ![设置Server站点用户名和密码](https://gitee.com/thiswildidea/images/blob/master/arcgisenterprise/install/linux/datastore/datastore1.png)
2 设置内容目录的位置，点击下一步。
 ![设置内容目录的位置](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/datastore/datastore2.png)

3 根据需要，选择配置关系型、切片缓存型和时空型的 Data Store，点击下一步。
 ![选择datastore类型](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/datastore/datastore3.png)
4 点击完成，直至安装成功。
![完成](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/datastore/datastore4.png)

## 安装和配置PortalforArcGIS
### 安装前准备
安装 dos2unix。
```bash
[root@agsenterprise arcgis]# yum install dos2unix
```
#### 诊断当前环境是否满足PortalforArcGIS安装要求
运行 portaldiag 脚本诊断当前环境是否满足 Portal for ArcGIS 的安装要求。

```bash
[arcgis@agsenterprise ~]$ PortalForArcGIS/portaldiag/portaldiag
```
当出现如下信息，说明当前环境满足需求，可安装 Portal for ArcGIS。
There were 0 failure(s) and 0 warning(s) found:

### 安装PortalforArcGIS
这里利用 console 模式进行交互安装。。
```bash
[arcgis@agsenterprise ~]$ cd PortalForArcGIS/
[arcgis@agsenterprise PortalForArcGIS]$ ./Setup -m console
```
安装完毕，显示如下信息，说明安装成功。
Congratulations. Portal for ArcGIS 10.7 has been successfully installed to:/home/arcgis/arcgis/portal
You will be able to access Portal for ArcGIS 10.7 by navigating to
https://localhost:7443/arcgis/home.

### 配置PortalforArcGIS
在浏览器中输入 Portal for ArcGIS 的访问地址
https://agsenterprise.shsmi.com:7443/arcgis/home/ ，开始进行 Portal for ArcGIS 的配置。
1 点击 CREATE NEW PORTAL
![创建portal](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/portal1.png)

2 设置初始管理员账户信息和 Portal for ArcGIS 站点的内容目录，点击 CREATE 开始创建。
![配置设置](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/portal2.png)
3 在弹出的 Account Created 界面上点击 OK，完成 Portal for ArcGIS 的配置 。页面自动导航至新的页面，要求配置 Web Adaptor。
![porta create successed](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/portal3.png)

##  安装和配置WebAdaptor
### 安装前准备
#### 安装JDK
##### 解压JDK
```bash
[root@agsenterprise home]# tar -zxvf jdk-8u111-linux-x64.tar.gz
[root@agsenterprise home]# mv jdk1.8.0_111/ jdk8
```
##### 配置JDK环境变量
1 编辑/etc/profile，配置 JDK 环境变量。
```bash
# /etc/profile
JAVA_HOME=/home/jdk8
CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/tools.jar
PATH=$JAVA_HOME/bin:$PATH
export JAVA_HOME CLASSPATH PATH
```
2 运行 source /etc/profile，使 JDK 环境变量配置生效。

3 验证 JDK 配置
```bash
[root@agsenterprise home]# java -version
```
java version "1.8.0_111"
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
出现上述信息，Java 版本是 1.8.0_111，说明 JDK 环境变量配置成功。
#### 安装tomcat
##### 解压tomcat
```bash
[root@agsenterprise home]# tar -zxvf apache-tomcat-8.0.32.tar.gz
[root@agsenterprise home]# mv apache-tomcat-8.0.32 tomcat8
```

##### 创建自签名证书
1 创建私钥和证书请求
```bash
[root@agsenterprise home]# openssl req -newkey rsa:2048 -nodes -keyout /home/tomcat8/agsenterprise.key -x509 -days 365 -out /home/tomcat8/agsenterprise.crt 
```
输入自签名证书创建所需的参数。创建自签名证书时，Common Name 输入的是当前机器
的完全限定域名即 agsenterprise.shsmi.com。
Country Name (2 letter code) [XX]:CN
State or Province Name (full name) :Beijing
Locality Name (eg, city) [Default City]:Beijing
Organization Name (eg, company) [Default Company Ltd]:shsmi
Organizational Unit Name (eg, section) :TechSupport
Common Name (eg, your name or your server's hostname) :agsenterpris
e.esrichina.com
Email Address test@qq.com

2 创建自签名证书
```bash
[root@agsenterprise home]# openssl pkcs12 -inkey /home/tomcat8/agsenterprise.key -in /home/tomcat8/agsenterprise.crt -export -out /home/tomcat8/agsenterprise.pfx 
```
##### 对tomcat启用ssl
编辑 tomcat 的 server.xml 文件，
1) 将 8080 端口号修改为 80；
2) 将 8443 端口修改为 443；
3) 取消端口号 8443 对应的 connector 的注释，并启用 ssl
```bash
[root@agsenterprise home]# vi tomcat8/conf/server.xml
```
1 将 8080 端口号修改为 80。
<Connector port="80" protocol="HTTP/1.1"
connectionTimeout="20000"
redirectPort="443" />
2 取消端口号 8443 对应的 connector 的注释，将 8443 端口修改为 443，并启用 ssl。
<Connector port="443" protocol="org.apache.coyote.http11.Http11Nio
Protocol"maxThreads="150" SSLEnabled="true" scheme="https" secure=
"true"  clientAuth="false" sslProtocol="TLS" keystoreFile="/home/
tomcat8/ssl/agsenterprise.pfx" keystoreType="pkcs12" keystorePass=
"shsmi@123" />

#####  启动和验证tomcat
运行 startup.sh 启动 tomcat。
```bash
[root@agsenterprise home]# cd tomcat8/bin/
[root@agsenterprise bin]# ./startup.sh
```
Using CATALINA_BASE: /home/tomcat8
Using CATALINA_HOME: /home/tomcat8
Using CATALINA_TMPDIR: /home/tomcat8/temp
Using JRE_HOME: /home/jdk8/jre
Using CLASSPATH: /home/tomcat8/bin/bootstrap.jar:/home/tomcat
8/bin/tomcat-juli.jar
Tomcat started.
验证 tomcat 启动是否成功。

### 安装和部署WebAdaptor
#### 安装WebAdaptor
 以静默模式安装 Web Adaptor。
 ```bash
 [arcgis@agsenterprise ~]$ WebAdaptor/Setup -m silent -l Yes
 ```
 看到如下信息，说明 Web Adaptor 安装成功。
...ArcGIS Web Adaptor (Java Platform) 10.7 installation is complete.

#### 部署WebAdaptor到tomcat下
依次部署名为 arcgis 和 server 的 Web Adaptor 应用到 tomcat 下，用于实现对 Portal for
ArcGIS 和 ArcGIS for Server 的配置。
 ```bash
[root@agsenterprise home]# cp /home/arcgis/webadaptor10.7/java/arcgis.war /home/tomcat8/webapps/arcgis.war
 ```
```bash
[root@agsenterprise home]# cp /home/arcgis/webadaptor10.7/java/arcgis.war /home/tomcat8/webapps/server.war
 ```
### 配置WebAdaptor
当通过浏览器对 Portal for ArcGIS 和 ArcGIS for Server 配置 Web Adaptor 时，要求必须在 Web Adaptor 所在的机器上。因此，
当从非 Web Adaptor 所在机器的其他客户端配置Web Adaptor时，需要以命令行的形式
对 Portal for ArcGIS 配置名为 arcgis 的 Web Adaptor
 ```bash
[arcgis@agsenterprise ~]$ cd webadaptor10.7/java/tools/
[arcgis@agsenterprise tools]$ ./configurewebadaptor.sh -m portal -w https://agsenterprise.shsmi.com/arcgis/webadaptor -g
 https://agsenterprise.shsmi.com:7443/ -u portaladmin -p shsmi@123 
 ```
返回** Successfully Registered.**说明配置成功，即可通过 webadaptor 访问 Portal for
ArcGIS。
![webdaptor for portal](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/webadaptor/portal.png)

对 ArcGIS for Server 配置名为 server 的 Web Adaptor
 ```bash
[arcgis@agsenterprise tools]$ ./configurewebadaptor.sh -m server -w https://agsenterprise.shsmi.com/server/webadaptor -g https://
agsenterprise.shsmi.com:6443 -u siteadmin -p shsmi@123 -a true
 ```
 返回** Successfully Registered.**说明配置成功，即可通过 webadaptor 访问 ArcGIS for
Server。
![webdaptor for arcgis server](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/webadaptor/agsserver.png)

### 实现Portal和Server的托管
 1.登录 Portal for ArcGIS
 ![settings for portal](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/setting1.png)
 2.依次点击 My Organization->EDIT SETTINGS->Servers，然后点击 ADD SERVER。
 3.在弹出的 Add ArcGIS Server 对话框上设置 Services URL、Administration URL，和主
站点管理员账户的用户名和密码，点击 ADD
 ![settings for portal](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/setting2.png)
 4.对 Hosting Server 选中联合的 Server，即 agsenterprise.esrichina.com/server。
 ![settings for portal](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/setting3.png)
 5.点击 SAVE 保存
## 补充
在单机环境下，为了确保 ArcGIS for Server、Portal for ArcGIS 和 Web 服务器三个层面证书的统一，可将 ArcGIS for Server 和 Portal for ArcGIS 的证书更新为 Web 服务器的同一证书。
### 对ArcGISforServer更新证书
1 访问 ArcGIS for Server 的 admin 页面，即 https://agsenterprise.shsmi.com:6443/arcgis/admin/，输入用户名和密码登录

2 导航至 machines -> Machines 下机器名，如 AGSENTERPRISE.SHSMI.COM ->
sslcertificates，点击 importExistingServerCertificate。输入 agsenterprise.pfx 的路径和密
码，设置证书别名，点击 Submit。
![更新 ageserver证书](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/certificate.png)
3 返回至 Machines - 机器名即 Machine - AGSENTERPRISE.SHSMI.COM 页面，
点击 edit
![更新 ageserver证书](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/certificate1.png)
4 在 Edit Machine 页面上，设置 Web server SSL Certificate 的值为步骤 2 中的证书别名如 agsenterprise 以引用上述证书，点击 Save Edits。
![更新 ageserver证书](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/arcgisserver/certificate2.png)
如上，完成了对 ArcGIS for Server 的证书更新
### 对PortalforArcGIS更新证书
1 访问 Portal for ArcGIS 的 admin 页面，
即 https://agsenterprise.esrichina.com/arcgis/portaladmin/ ，输入用户名和密码登录。
2 导航至 security -> sslCertificates，点击 importExistingServerCertificate。输入agsenterprise.pfx 的路径和密码，设置证书别名，点击 import。
![更新 protal 证书](https://gitee.com/thiswildidea/images/raw/master/arcgisenterprise/install/linux/portal/certifize.png)
3 在 sslCertificate 页面上点击 Update。
4 在 Update Web Server Certificate 页面上，输入步骤 2 中的证书别名引用上述证书，点击 Update。如上，完成了对 Portal for ArcGIS 的证书更新。
![更新 protal 证书](https://gitee.com/thiswildidea/images/blob/master/arcgisenterprise/install/linux/portal/certifize1.png)

### 在客户端机器上安装证书
将证书安装到计算机的受信任的根证书颁发机构。
1 在浏览器中打开 Portal for ArcGIS，如
https://agsenterprise.shsmi.com/arcgis/home/。

2 点击 Internet 选项 -> 安全，选中 受信任的站点，点击 站点，
将 https://agsenterprise.shsmi.com 添加 到 受信任的站点 列表。
