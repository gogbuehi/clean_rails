CLEAN RAILS Vagrant Box
=======================

This is a simple repository for creating a simple rails app.

Requirements
------------
 - VirtualBox
 - Vagrant

Command-line steps:
-------------------
 1. Clone this repository and navigate to the directory
 2. Run `vagrant up`
 3. Run `vagrant ssh`
 4.     `cd /vagrant`
 5.     `gem install rails`
 6.     `rails new .`

Start Rails without a DB
---------------------
 - Remove database adapter gems from your Gemfile (mysql2, sqlite3, etc.)
 - Change your config/application.rb in the following way:
   * Remove require 'rails/all line and require frameworks you want to use, for example:

     * require "action_controller/railtie"
     * require "action_mailer/railtie"
     * require "sprockets/railtie"
     * require "rails/test_unit/railtie"

   * Note: I put these 4 in mine; Got the solution from here http://stackoverflow.com/questions/19078044/disable-activerecord-for-rails-4 (Step 1 and 2 were all I needed)

Configure Rails with a MySQL DB
-------------------------------
 - In your `Gemfile`, make sure to have the following lines:

   * `gem 'mysql2'`
   * `gem 'activerecord'`

 - If you started the project without a DB (as described above), reverse the steps in `config/application.rb`:

   * Remove references to specific rails components. i.e.:

     * `require "action_controller/railtie"`
     * `require "action_mailer/railtie"`
     * etc...

    * In place of those, put in `require "rails/all"`

 - Set up your database configuration in `config/database.yml`

Example `database.yml`
----------------------

```
default: &default
  adapter: mysql2
  encoding: utf8

# If your DB is not running inside the same virtual machine, 
# you may need to use you host machine's IP address, 
# instead of 127.0.0.1

development:
  <<: *default
  database: my_rails_db
  username: dev_username
  password: SUPER_SECRET_PASSW0RD
  host: 10.0.2.2
  port: 3306

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: db_test
  username: root
  password: test_db_password


dev1:
  <<: *default
  database: 'heroku_dev12345'
  username: ENV['DB_USER']
  password: ENV['DB_PASS']
  host: ENV['DATABASE_URL']
  port: 3306


production:
  <<: *default
  database: 'heroku_prod12345'
  username: ENV['DB_USER']
  password: ENV['DB_PASS']
  host: ENV['DATABASE_URL']
  port: 3306
```

 - Ensure your database is up and running before starting rails

 - The rails app should start up fine, if it is able to connect to the database. Otherwise, it will give an error, if there is an issue connecting to it.

Starting Rails
--------------
Use the following command within the virtual machine in `/vagrant/`:
 - `rails s -b 0.0.0.0 -p 3001`

Go to the following URL in a browser:
 - http://localhost:4513/

TODO Items
==========

 - Instructions on setting up initial models with ActiveRecord
 - Instructions on setting up initial routes and controllers
