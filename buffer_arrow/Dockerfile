FROM ruby:latest

RUN \
  apt update && \
  apt install -y -V \
    apt-transport-https \
    curl \
    gnupg \
    lsb-release && \
  distribution=$(lsb_release --id --short | tr 'A-Z' 'a-z') && \
  code_name=$(lsb_release --codename --short) && \
  curl --output /usr/share/keyrings/apache-arrow-keyring.gpg \
    https://apache.bintray.com/arrow/${distribution}/apache-arrow-keyring.gpg && \
  echo "deb [signed-by=/usr/share/keyrings/apache-arrow-keyring.gpg] https://apache.bintray.com/arrow/${distribution}/ ${code_name} main" > \
    /etc/apt/sources.list.d/apache-arrow.list && \
  apt update && \
  gem install red-parquet && \
  apt clean && \
  rm -rf /var/lib/apt/lists/*

COPY . /fluentd-benchmark
WORKDIR /fluentd-benchmark

RUN bundle install
