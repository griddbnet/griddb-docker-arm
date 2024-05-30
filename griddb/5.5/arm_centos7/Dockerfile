FROM centos:centos7

# You can download griddb V5.5.0 directly at https://github.com/griddb/griddb/releases/tag/v5.5.0
ENV GRIDDB_VERSION=5.5.0
ENV GRIDDB_DOWNLOAD_SHA512=31c5dc1589e5f782687c0db55fd3daa4e3abb7a3c006360729e18461501fbe5cb1a3f3ace962a84858e26466cccfce91cee0265077af3ac2a2797ec27e8fb281
ENV GS_HOME=/var/lib/gridstore
# Need declare $GS_LOG to start GridDB server
ENV GS_LOG=/var/lib/gridstore/log
ENV PORT=10001

COPY griddb-${GRIDDB_VERSION}-linux.aarch64.rpm  /
RUN set -eux \
    && yum -y update 
    # Install dependencies for griddb
RUN yum install -y wget python3 epel-release \
    && yum install -y jq \
    && yum clean all 
    # Install package griddb server
RUN rpm -i /griddb-${GRIDDB_VERSION}-linux.aarch64.rpm \
    # Remove package
    && rm /griddb-${GRIDDB_VERSION}-linux.aarch64.rpm

VOLUME $GS_HOME
WORKDIR $GS_HOME

COPY start-griddb.sh /
USER gsadm
ENTRYPOINT ["/bin/bash", "/start-griddb.sh"]
EXPOSE $PORT
CMD ["griddb"]
