FROM debian:13-slim

# install useful packages
RUN set -eux; \
  \
  apt-get update; \
  apt-get install -y --no-install-recommends \
  build-essential \
  byobu \
  ca-certificates \
  curl \
  default-libmysqlclient-dev \
  default-mysql-client \
  dnsutils \
  git \
  inetutils-ping \
  inetutils-telnet \
  inetutils-tools \
  inetutils-traceroute \
  less \
  libpq-dev \
  nano \
  postgresql-client \
  python-is-python3 \
  python3 \
  python3-dev \
  python3-pip \
  python3-setuptools \
  redis-tools \
  ruby \
  ruby-dev \
  screen \
  ssh-client \
  telnet \
  unzip \
  vim \
  wget \
  zstd \
  ; \
  rm -rf /var/lib/apt/lists/*

# install yq - https://github.com/mikefarah/yq
RUN set -eux; \
  \
  wget https://github.com/mikefarah/yq/releases/latest/download/yq_linux_amd64 -O /usr/local/bin/yq; \
  chmod +x /usr/local/bin/yq

# install duckdb - https://duckdb.org/
RUN set -eux; \
  \
  curl https://install.duckdb.org | sh; \
  ln -s /root/.duckdb/cli/latest/duckdb /usr/local/bin/duckdb

# skip installing gem documentation with `gem install`/`gem update`
RUN set -eux; \
  mkdir -p /usr/local/etc; \
  echo 'gem: --no-document' >> /usr/local/etc/gemrc

# install useful ruby gems
RUN set -eux; \
  \
  gem install -N \
  bundler \
  http \
  mysql2 \
  pg \
  redis \
  sequel \
  ;

# run all scripts in /etc/console/init/boot.d
RUN set -eux; \
  test ! -d /etc/console/init/boot.d || find /etc/console/init/boot.d -maxdepth 1 -type f -exec bash {} \;

# sleep forever
CMD ["/bin/sh", "-c", "--", "sleep infinity"]
