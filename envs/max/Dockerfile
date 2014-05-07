FROM upcnet/base:precise-py27
RUN mkdir /var/max.docker.local
WORKDIR /var/max.docker.local
RUN git clone https://github.com/UPCnet/maxserver root
WORKDIR /var/max.docker.local/root
RUN /var/pyramid/python2.7/bin/python bootstrap.py -c max-only.cfg
RUN /var/max.docker.local/root/bin/buildout -c max-only.cfg
CMD /bin/bash
