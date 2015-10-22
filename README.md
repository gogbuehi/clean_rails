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

FOLLOW THESE STEPS TO START RAILS WITH NO DB
--------------------------------------------
 - Remove database adapter gems from your Gemfile (mysql2, sqlite3, etc.)
 - Change your config/application.rb in the following way:
 -- Remove require 'rails/all line and require frameworks you want to use, for example:

 --- require "action_controller/railtie"
 --- require "action_mailer/railtie"
 --- require "sprockets/railtie"
 --- require "rails/test_unit/railtie"

 -- Note: I put these 4 in mine; Got the solution from here http://stackoverflow.com/questions/19078044/disable-activerecord-for-rails-4 (Step 1 and 2 were all I needed)

STARTING RAILS
--------------
USE THE FOLLOWING COMMAND WITHIN THE VIRTUAL MACHINE IN `/vagrant/`:
 - `rails s -b 0.0.0.0 -p 3001`

GO TO THE FOLLOWING URL IN A BROWSER:
http://localhost:4513/

TODO ITEMS
==========

 - Instructions on connecting to a MySQL DB
