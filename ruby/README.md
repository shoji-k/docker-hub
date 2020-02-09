## start new project

Create new Rails code, this also creates .git

```bash
$ docker-compose run --rm web rails new . --force --no-deps --database=postgresql --api
$ sudo chown -R $USER:$USER .
```

Prepare database setting

```bash
vim confing/database.yml
```

```yml
default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  host: <%= ENV.fetch("RAILS_DATABASE_HOST") %>
  username: <%= ENV.fetch("RAILS_DATABASE_USER") %>
  password: <%= ENV.fetch("RAILS_DATABASE_PASSWORD") %>

development:
  <<: *default
  database: development

test:
  <<: *default
  database: test

production:
  <<: *default
  database: production
```

Save code in container


```bash
$ docker-compose build
```

Run and prepare db

```bash
$ docker-compose up
$ docker-compose run --rm web rails db:create
```

Remove the old image, the old one name is none

```bash
REPOSITORY               TAG                 IMAGE ID            CREATED             SIZE
ruby_web                 latest              8059627517a8        19 seconds ago      1.02GB
<none>                   <none>              4dfa30db4f0d        4 minutes ago       984MB
```

if you want to run rails db:migrate

```bash
$ docker-compose run --rm web rails db:migrate
```

if you change Gemfile, rebuild image

```bash
$ docker-compose run --rm web bundle install
$ docker rmi ruby_web
$ docker-compose build
```

if you clean all

```bash
$ docker-compose down -v
```

## start when rails codes are ready

copy files here except for README.md, Gemfile and Gemfile.lock.  
And improve .dockerignore for your project.  
Then build.

```bash
$ docker-compose build
```

Run

```bash
$ docker-compose up
```
