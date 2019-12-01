FROM ruby:2.6

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs \
    locales task-japanese sqlite3 libsqlite3-dev
# locales task-japanese # for locale

# ADD Gemfile /myapp/Gemfile
# ADD Gemfile.lock /myapp/Gemfile.lock
# RUN bundle install --path vendor/bundle

# ENV LANG ja_JP.UTF-8
# ENV LANGUAGE ja_JP:ja
# ENV LC_ALL ja_JP.UTF-8
# RUN sed -i -e 's/# ja_JP.UTF-8 UTF-8/ja_JP.UTF-8 UTF-8/' /etc/locale.gen && \
#   echo 'LANG="ja_JP.UTF-8"'>/etc/default/locale && \
#   locale-gen ja_JP.UTF-8 && \
#   DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

# echo "Asia/Tokyo" > /etc/timezone && \
# dpkg-reconfigure -f noninteractive tzdata && \

ENV BUNDLER_VERSION=2.0.2

ENV LANG=C.UTF-8\
  GEM_HOME=/bundle\
  BUNDLE_JOBS=4\
  BUNDLE_RETRY=3
ENV BUNDLE_PATH $GEM_HOME
ENV BUNDLE_APP_CONFIG=$BUNDLE_PATH\
  BUNDLE_BIN=$BUNDLE_PATH/bin
ENV PATH /app/bin:$BUNDLE_BIN:$PATH

RUN gem update --system &&\
    gem install bundler:$BUNDLER_VERSION &&\
    gem install rails &&\
    mkdir -p /app

WORKDIR /app
