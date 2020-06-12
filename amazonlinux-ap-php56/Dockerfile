FROM amazonlinux:2018.03
MAINTAINER Shin <hiep@verve-inc.jp>

# Set Japanese locale
RUN localedef -f UTF-8 -i ja_JP ja_JP.utf8

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
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm \
  && yum install -y http://rpms.remirepo.net/enterprise/remi-release-6.rpm

# Install apache
RUN yum update -y && yum install -y httpd mod_ssl && yum clean all

RUN yum update -y && \
  yum install -y --disablerepo=amzn-main  --enablerepo=epel libwebp \
  && yum clean all

RUN yum update -y && yum install -y \
  ncurses-compat-libs \
  libxml2 \
  libXpm \
  gmp \
  libicu \
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
  gd-last \
  zip \
  unzip \
  tar \
  && yum clean all

RUN yum update -y && \
  yum install -y --enablerepo=remi,remi-php56 t1lib \
  && yum clean all


RUN yum update -y \
  && yum install -y --disablerepo=amzn-main,amzn-updates --enablerepo=remi,remi-php56 \
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
