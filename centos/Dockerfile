FROM centos:7.6.1810
MAINTAINER "isun"
LABEL components="centos7, net-tools, nginx"

ENV LANG en_US.UTF-8
ENV CENTOS_VERSION=7.6.1810

# 配置时区
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

# 安装net-tools
RUN yum install net-tools -y 

# 引入Nginx主版本yum源
RUN echo $'\
[nginx-mainline] \n\
name=nginx mainline repo \n\
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/ \n\
gpgcheck=1 \n\
enabled=1 \n\
gpgkey=https://nginx.org/keys/nginx_signing.key \n\
module_hotfixes=true\
' > /etc/yum.repos.d/nginx.repo

# 安装nginx
RUN yum install nginx -y

# 将Nginx日志链接到标准输入输出
RUN ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

# 容器端口为80
EXPOSE 80
STOPSIGNAL SIGTERM

# 将Nginx版本号加到环境变量
ENV NGINX_VERSION=1.17.6

# 在前台启动
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
