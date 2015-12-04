FROM index.alauda.cn/toughstruct/tough-pypy
MAINTAINER jamiesun <583037724@qq.com>


ADD ./radiusd.conf /etc/radiusd.conf
ADD ./supervisord.conf /etc/supervisord.conf
ADD ./toughrad /usr/bin/toughrad

RUN chmod +x /usr/bin/toughrad

ADD ./privkey.pem /var/toughradius/privkey.pem
ADD ./cacert.pem /var/toughradius/cacert.pem


RUN git clone -b master https://github.com/davislidaqing/Mcoderadius.git /opt/toughradius
RUN ln -s /opt/toughradius/toughctl /usr/bin/toughctl && chmod +x /usr/bin/toughctl

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN pypy /opt/toughradius/toughctl --initdb

RUN echo "set nocompatible" >> /root/.vimrc && echo "set backspace=2" >> /root/.vimrc

EXPOSE 1815 1816 1817 1819
EXPOSE 1812/udp
EXPOSE 1813/udp

VOLUME [ "/var/toughradius" ]
ENTRYPOINT ["/usr/bin/toughrad","start"]

