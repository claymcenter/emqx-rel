FROM debian:7

RUN apt-get update \
    && apt-get install -y wget git zip  build-essential debhelper libncurses5-dev unixodbc unixodbc-dev openjdk-7-jdk libssl-dev curl
RUN wget http://erlang.org/download/otp_src_21.0.tar.gz &&  tar zxvf otp_src_21.0.tar.gz && cd otp_src_21.0 && ./configure && make && make install
RUN mkdir -p /root/.ssh/
# cleanup
RUN apt-get clean\
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /otp_src_21.0/* /otp_src_21.0.tar.gz

ADD ./files/id_rsa /root/.ssh/
ADD ./files/id_rsa.pub /root/.ssh/
ADD ./files/config /root/.ssh/
ADD ./files/emqx_ci.sh /
ADD ./files/emqx_nightly_ci.sh / 
ADD ./files/emqx_release_ci.sh /

RUN chmod +x /emqx_ci.sh /emqx_nightly_ci.sh /emqx_release_ci.sh

CMD ["/emqx_ci.sh"]
