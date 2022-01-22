# CreateRailsApp

Create a new rails application with all its dependencies in a couple of minutes.

## Using Docker
- Create your app folder
  ```
  mkdir my_new_app && cd my_new_app 
  ```
- Clone repo or Download [Dockerfile](Dockerfile) and [docker-compose.yml](docker-compose.yml) inside the new folder
- (Optional) Edit `docker-compose.yml` to use Mysql instead of Postgres
    - Enable Mysql image (uncomment lines from 5 until 11) and enable volume in line 51
    - Disable Postgres image (comment lines from 21 until 29) and disable volume in line 50
    - Replace `postgres` for `mysql` inside `depends_on` (Line 38)
- Build the container
  ```
  docker-compose run --service-ports app bash
  ```
- Create the new application (See all options with `rails new --help` and customize based on it)
  ```
  rails new . --database=postgresql --javascript=esbuild --css=sass
  ```
- Edit DB settings    
  Edit `config/database.yml` and enter the database credentials (`host: postgres`, `username: root`, `password: password` By default defined in docker-compose.yml)

- Edit `Procfile.dev` to add `-b 0.0.0.0`, should look like: `web: bin/rails server -p 3000 -b 0.0.0.0` (Fix: Localhost domain name)

- Run application
  ```
  rails db:create
  bin/dev
  ```
  Visit http://localhost:3000
  
## Extra
- Enable `redis` image in docker-compose.yml for the following cases:
  -  ActionCable
  -  TurboStream
  -  Caching
  -  Background jobs
- Use the following redis url (Note hostname is `redis`): `redis://redis:6379/0`
