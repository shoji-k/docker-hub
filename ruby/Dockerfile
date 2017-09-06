FROM ruby

RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs locales \
  && mkdir /myapp \
  && locale-gen ja_JP.UTF-8

WORKDIR /myapp

ADD Gemfile /myapp/Gemfile
ADD Gemfile.lock /myapp/Gemfile.lock

RUN bundle install

ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
