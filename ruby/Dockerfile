FROM ruby:2.6.5

ENV APP_HOME /app

RUN apt-get update -qq \
  && apt-get install -y nodejs postgresql-client --no-install-recommends \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
RUN mkdir $APP_HOME
WORKDIR $APP_HOME

RUN gem install bundler -v '2.1.4'

COPY Gemfile $APP_HOME/Gemfile
COPY Gemfile.lock $APP_HOME/Gemfile.lock
RUN bundle install
COPY . $APP_HOME

COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

CMD ["rails", "server", "-b", "0.0.0.0"]
