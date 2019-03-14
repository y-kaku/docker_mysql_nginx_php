FROM centos:centos7

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN yum -y install wget epel-release

RUN wget http://rpms.famillecollet.com/enterprise/remi-release-7.rpm
RUN rpm -Uvh ./remi-release-7.rpm
RUN sed -i '4a priority=1' /etc/yum.repos.d/remi-php71.repo
RUN yum -y install --enablerepo=remi-php71 php php-fpm php-mcrypt php-cli php-common php-devel php-gd php-mbstring php-mysqlnd php-opcache php-pdo php-pear php-pecl-apcu php-pecl-zip php-process php-xml
RUN yum clean all

RUN yum install -y httpd && systemctl enable httpd.service
RUN yum clean all

RUN yum -y update
RUN yum clean all

RUN yum -y install git

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION v6.10.3

RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.26.1/install.sh | bash \
    && source ~/.bashrc \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default

EXPOSE 80

#CMD ["systemctl enable httpd"]

#CMD ["systemctl", "start",  "httpd.service"]
CMD /sbin/init
