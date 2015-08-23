FROM chenhuimin/serf-dnsmasq:1.0

MAINTAINER chenhuimin <chenhuimin66@gmail.com>

# install openssh-server, vim and openjdk
RUN apt-get install -y openssh-server vim
#RUN apt-get install -y openjdk-7-jdk 
# java
RUN curl -LO 'http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.rpm' -H 'Cookie: oraclelicense=accept-securebackup-cookie'
RUN rpm -i jdk-7u71-linux-x64.rpm
RUN rm jdk-7u71-linux-x64.rpm

# move all configuration files into container
ADD files/* /usr/local/  

# set jave environment variable 
#ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64 
#ENV PATH $PATH:$JAVA_HOME/bin

ENV JAVA_HOME /usr/java/default
ENV PATH $PATH:$JAVA_HOME/bin

#configure ssh free key access
RUN mkdir /var/run/sshd && \
ssh-keygen -t rsa -f ~/.ssh/id_rsa -P '' && \
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys && \
mv /usr/local/ssh_config ~/.ssh/config && \
sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

#install hadoop 2.30
#RUN ln -s /usr/local/hadoop-2.3.0 /usr/local/hadoop && \
# install hadoop 2.7.0
RUN ln -s /usr/local/hadoop-2.7.0 /usr/local/hadoop && \
mv /usr/local/bashrc ~/.bashrc && \
mv /usr/local/hadoop-env.sh /usr/local/hadoop/etc/hadoop/hadoop-env.sh 
