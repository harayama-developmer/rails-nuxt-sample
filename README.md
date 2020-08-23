# README

Rails API + Nuxt on Docker.

[![Image from Gyazo](https://i.gyazo.com/c04984a2a06fb3569c9062433119e8c8.png)](https://gyazo.com/c04984a2a06fb3569c9062433119e8c8)

## Setup

```bash
$ mkdir YOUR_PROJECT
$ cd YOUR_PROJECT
$ git clone git@github.com:harayama-developmer/rails-nuxt-template.git .

$ rm -rf .git/

# Rails Setup
$ rm backend/config/credentials.yml.enc
$ docker-compose run --rm backend rails credentials:edit
#=> create  config/master.key

# Nuxt Setup
$ touch frontend/.env
#=> Edit .env below
# BASE_URL=http://localhost:3000
# API_URL=http://backend:3000
# API_URL_BROWSER=http://localhost:3000

$ docker-compose build
$ docker-compose run --rm backend bundle exec rails db:setup
$ docker-compose up
```

Access in browser!

- Nuxt: http://localhost:8080
- Rails: http://localhost:3000

### Sample CRUD page

http://localhost:8080/events

Table:

```
create_table "events", force: :cascade do |t|
  t.string "name"
  t.datetime "created_at", precision: 6, null: false
  t.datetime "updated_at", precision: 6, null: false
end
```

[![Image from Gyazo](https://i.gyazo.com/d68d89fba3c81aeebd413096b242d517.png)](https://gyazo.com/d68d89fba3c81aeebd413096b242d517)