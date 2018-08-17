FROM debian:8.10

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        gcc \
        g++ \
        git \
        graphviz \
        libelf-dev \
        libmysqlclient-dev \
        libreadline-dev \
        libssl-dev \
        make \
        nodejs \
        npm \
        ocaml \
        wget \
        zlib1g-dev

ENV RUBY_MAJOR   2.5
ENV RUBY_VERSION 2.5.0

RUN wget -O ruby.tar.gz "https://cache.ruby-lang.org/pub/ruby/$RUBY_MAJOR/ruby-$RUBY_VERSION.tar.gz" && tar xvzf ruby.tar.gz
RUN cd ruby-* && ./configure && make && make install && cd - && rm -rf ruby*

ENV RUBYGEMS_VERSION 2.7.7
RUN gem update --system "$RUBYGEMS_VERSION"

ENV BUNDLER_VERSION 1.16.2
RUN gem install bundler --version "$BUNDLER_VERSION" --no-document --force
RUN bundle config --global jobs 4

ENV NODE_VERSION 10.5.0
RUN npm install -g n && n $NODE_VERSION

ENV YARN_VERSION 1.8.0
RUN npm install -g "yarn@${YARN_VERSION}"

RUN rm -rf /var/lib/apt/lists/*

RUN useradd -m webapp
RUN mkdir -p /repos/webapp
RUN chown -R  webapp:webapp /repos

USER webapp
WORKDIR /repos/webapp

EXPOSE 3000

