
#
#创建带sshd的镜像  
#docker version 1.12 build image centos7.1-sshd  from centos7.1 

FROM europeanspallationsource/centos7.1-base7-epel7
MAINTAINER heweijun <heweijun@icyun.com>

RUN yum -y  update 
RUN yum -y  upgrade
RUN yum -y  install openssh-server
RUN yum -y  install vim
#修改/etc/ssh/sshd_config
RUN sed -i 's/UsePAM yes/UsePAM no/g' /etc/ssh/sshd_config
#将密钥文件复制到/etc/ssh/目录中
ADD id_rsa /etc/ssh/ssh_host_rsa_key
ADD id_rsa.pub /etc/ssh/ssh_host_rsa_key.pub
RUN mkdir -p /root/.ssh
ADD authorized_keys /root/.ssh/authorized_keys
#将ssh服务启动脚本复制到/usr/local/sbin目录中，并改变权限为755
ADD run.sh /usr/local/sbin/run.sh
RUN chmod 755 /usr/local/sbin/run.sh
#变更root密码为147258
RUN echo "root:147258"|chpasswd
#开放窗口的22端口
EXPOSE 22
#运行脚本，启动sshd服务
CMD ["/usr/local/sbin/run.sh"]



