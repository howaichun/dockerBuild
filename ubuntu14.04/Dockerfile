FROM ubuntu
MAINTAINER heweijun<heweijun@iciyun.com>


CMS echo ubuntu:14.04 purity image


# 更新源，安装ssh server
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe"> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd

# 设置root ssh远程登录密码为123456
RUN echo "root:123456" | chpasswd 

RUN apt-get install python-software-properties
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update

# 设置JAVA_HOME环境变量
RUN update-alternatives --display java

# 容器需要开放SSH 22端口
EXPOSE 22

# 容器需要开放Tomcat 8080端口
EXPOSE 8080

# 设置Tomcat7初始化运行，SSH终端服务器作为后台运行
ENTRYPOINT service tomcat9 start && /usr/sbin/sshd -D
