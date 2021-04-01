FROM centos:7 AS base

#add dinstall group
RUN groupadd dinstall && useradd -g dinstall -m -d /home/dmdba -s /bin/bash dmdba

FROM base AS install

#copy install files
ARG installFilesDir=/home/dmdba/install
ARG installConfName=setup.xml

COPY DMInstall.bin  ${installFilesDir}/
COPY ${installConfName} ${installFilesDir}/

#change user.DAMENG recommend installing with noroot
USER dmdba

#prepare install diretory
RUN mkdir /home/dmdba/dmdbms

#execute silence install
RUN sh ${installFilesDir}/DMInstall.bin -q ${installFilesDir}/${installConfName}

FROM base

# add gosu
RUN yum install -y wget && wget https://github.com/tianon/gosu/releases/download/1.11/gosu-arm64 \
    &&mv gosu-arm64 /usr/local/bin/gosu \
    &&chmod +x /usr/local/bin/gosu

RUN gosu dmdba mkdir /home/dmdba/dmdbms
COPY --from=install /home/dmdba/dmdbms /home/dmdba/dmdbms

#RUN /home/dmdba/dmdbms/script/root/root_installer.sh
RUN cp "/home/dmdba/dmdbms/bin/dm_svc.conf" /etc/dm_svc.conf
RUN chmod 6755 "/home/dmdba/dmdbms/bin/dminit" \
    && chmod 6755 "/home/dmdba/dmdbms/bin/dmserver" \
    && chown 0:0 "/home/dmdba/dmdbms/bin/dmcss" \
    && chmod 6755 "/home/dmdba/dmdbms/bin/dmcss"


COPY docker-entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

EXPOSE 5236

WORKDIR /home/dmdba

ENTRYPOINT ["docker-entrypoint.sh"]
