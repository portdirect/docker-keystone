FROM debian:jessie

ENV VIRTUAL_ENV /virtualenv
ENV PATH "$VIRTUAL_ENV/bin:$PATH"
COPY downloader.sh /
RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends \
		apache2 \
		ca-certificates \
		curl \
		libapache2-mod-wsgi \
	&& curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
	&& python get-pip.py \
	&& rm get-pip.py \
	&& pip install virtualenv \
	&& /downloader.sh \
	&& virtualenv $VIRTUAL_ENV \
	&& hash -r \
	&& pip install -c /tmp/packages/upper-constraints.txt --no-compile --find-links /tmp/packages http://tarballs.openstack.org/keystone/keystone-master.tar.gz \
	&& apt-get purge -y --auto-remove \
		ca-certificates \
		curl \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /root/.cache /usr/local/*