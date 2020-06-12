FROM amazonlinux:2
MAINTAINER Shin <hiep@verve-inc.jp>

# Set Japanese locale
RUN yum install -y glibc-langpack-ja && yum clean all
ENV LANG ja_JP.utf8
ENV LC_ALL ja_JP.utf8
RUN ln -snf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# Install base package
RUN yum update -y && yum install -y \
  sudo \
  vim \
  git \
  openssl-devel \
  yum-utils \
  curl \
  wget \
  && yum clean all

# Create user
RUN useradd -m ec2-user \
  && usermod -aG wheel ec2-user \
  && sed -i "s|# %wheel  ALL=(ALL) NOPASSWD: ALL|%wheel  ALL=(ALL) NOPASSWD: ALL|g" /etc/sudoers

# Install extra repo
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
  && yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm \
  && yum-config-manager --enable epel remi

# Install apache
RUN yum update -y && yum install -y httpd mod_ssl && yum clean all

# Install php
RUN yum update -y && yum install -y \
  ncurses-compat-libs \
  libxml2 \
  libXpm \
  gmp \
  libicu \
  t1lib \
  aspell \
  openssl \
  bzip2 \
  libcurl \
  libjpeg \
  libvpx \
  libpng \
  freetype \
  fontconfig \
  readline \
  libtidy \
  libxslt \
  libmcrypt \
  pcre \
  gettext \
  net-snmp \
  libevent \
  libtool-ltdl \
  libc-client \
  libmemcached \
  libtiff \
  zip \
  unzip \
  tar \
  && yum clean all

RUN yum update -y \
  && yum install -y --disablerepo=amzn2-core --enablerepo=remi-php56 \
  php \
  php-cli \
  php-common \
  php-gd \
  php-mbstring \
  php-mcrypt \
  php-mysqlnd  \
  php-pdo \
  php-pecl-igbinary \
  php-pecl-jsonc \
  php-pecl-memcached \
  php-pecl-msgpack \
  php-pecl-zip \
  php-process \
  php-xml \
  && yum clean all

COPY php.ini /etc/

RUN rm -f /etc/httpd/conf.d/ssl.conf

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]

EXPOSE 80
EXPOSE 443
