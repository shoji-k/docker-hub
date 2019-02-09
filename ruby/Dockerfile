FROM ruby:2.6

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs \
    locales task-japanese sqlite3 libsqlite3-dev
# locales task-japanese # for locale

RUN mkdir /myapp
WORKDIR /myapp

# ADD Gemfile /myapp/Gemfile
# ADD Gemfile.lock /myapp/Gemfile.lock
# RUN bundle install --path vendor/bundle

ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
RUN sed -i -e 's/# ja_JP.UTF-8 UTF-8/ja_JP.UTF-8 UTF-8/' /etc/locale.gen && \
  echo 'LANG="ja_JP.UTF-8"'>/etc/default/locale && \
  locale-gen ja_JP.UTF-8 && \
  DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales

# echo "Asia/Tokyo" > /etc/timezone && \
# dpkg-reconfigure -f noninteractive tzdata && \
