FROM centos:7

RUN yum -y install epel-release centos-release-scl-rh && \
		yum -y install rh-ruby25-ruby rh-ruby25-ruby-devel rh-ruby25-rubygem-bundler && \
		yum -y install git make gcc-c++ bzip2 && \
		yum -y install libvirt-devel postgresql-devel mysql-devel sqlite-devel && \
		yum -y install libxslt-devel systemd-devel libxml2-devel libcurl-devel && \
		yum -y install nodejs npm && \
		yum clean all

ADD ./container-assets/scl_enable.sh /etc/profile.d/scl_enable.sh

RUN useradd -u 1001 jenkins1
RUN usermod -aG wheel jenkins1

RUN useradd -u 1010 jenkins2
RUN usermod -aG wheel jenkins2

RUN git clone https://github.com/theforeman/foreman /root/foreman
WORKDIR /root/foreman

RUN scl enable rh-ruby25 'bundle install --path /opt/bundle'
RUN scl enable rh-ruby25 'npm install'

RUN mv node_modules /opt
RUN chmod 777 -R /opt/node_modules
RUN chmod 777 -R /opt/bundle
