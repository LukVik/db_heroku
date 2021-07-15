# Establishing a Ruby on Rails project DB on a Mac
_Installation of Ruby on Rails dependencies, remote control and deploy_
# Dependencies Ruby Mine:
https://www.jetbrains.com/help/ruby/set-up-a-ruby-development-environment.html

### How to install Rails
https://patilshekhar900.medium.com/how-to-install-rails-6-0-1112343183bb

### How to install Postgresql with Homebrew on Mac
https://www.moncefbelyamani.com/how-to-install-postgresql-on-a-mac-with-homebrew-and-lunchy/    
In Postgresql Wiki: https://wiki.postgresql.org/wiki/Homebrew  
How to start / stop Postgresql  
https://tableplus.com/blog/2018/10/how-to-start-stop-restart-postgresql-server.html   
How check postgres version:    
https://phoenixnap.com/kb/check-postgresql-version)  
Install Homebrew:    
https://brew.sh  
Install RVM and Development environment with connect to Git:
https://www.moncefbelyamani.com/how-to-install-xcode-homebrew-git-rvm-ruby-on-mac/ 
## Things you may want to cover:
To get started with the app, clone the repo and then install the needed gems:
- Ruby version: RVM ruby '2.6.5' change to '3.0.0'
- Rails version: '6.0.0'
- Database type: Postgresql
- System dependencies, recommended editor: Apple, Install RubyMine﻿
# CONFIGURATION:
## Install Ruby  
You may already have Ruby installed on your computer. You can check inside a terminal emulator by typing:  
$ rvm v

This should output some information on the installed Ruby version. If you have not yet there are two ways to install Ruby:    
$ ruby-install ruby
 or you can define ruby version:
$ ruby-install ruby 2.6.5  
$ rvm list  
$ rvm list known  
$ rvm get stable (ruby 3.0.0 was missing)  
$ rvm reload  
$ rvm use 3.0.0 --default  

Or with [Install RVM](https://rvm.io/rvm/install)  
$ rvm install "ruby-3.0.0"

In the RubyMine or other your editor choose SDK, Ruby 2.6.5 and Apply it, then in terminal or go Tools > Bundler > Install:  
$ bundle install
## Install Bundler:
If you have not yet bundler:  
$ gem install bundler  
$ bundle init  
$ bundle install  

## Install Rails:
Rails version is listed in gemfile.rb file. How version you are using check with command:  
$ rails -v 

Install version 6.0.0. by using Bundler (Tools > Bundler > Bundle install in RM). If you have not yet Rails version 6.0.0 Install Rails you can use command:  
$ gem install rails -v 6.0.0

# DATABASE:
You may already have Posgres installed on your computer. How version you are using check with command:  
$ postgres --version
## Install database tools:
1) **Install Homebrew**  
$ /bin/bash -c "$(curl -fsSL  
https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
2) **Update Homebrew**  
Before you install anything with Homebrew, you should always make sure it's up to date and that it's healthy:
$ brew update  
$ brew doctor  
3) **Install Postgres**  
$ brew install postgresql  
4) **Create/Upgrade a database**  
If this is your first time installing Postgres with Homebrew, you'll need to create a database with:  
$ initdb /usr/local/var/postgres -E utf8
5) **Start Postgres**  

_To start manually:_  
$ pg_ctl -D /usr/local/var/postgres start

_To stop manually:_  
$ pg_ctl -D /usr/local/var/postgres stop  

_To start PostgreSQL server now and relaunch at login:_  
$ brew services start postgresql  
$ psql postgres  

_And stop PostgreSQL:_  
brew services stop postgresql  
# Install JavaScript tools:
$ curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -  
$ echo ‘deb https://dl.yarnpkg.com/debian/ stable main’ | sudo tee /etc/apt/sources.list.d/yarn.list  
$ sudo apt update && sudo apt install yarn  
$ rails webpacker:install  

Make sure all packages are up to date using the following command.  
$ yarn install --check-files

Now start your rails server once again and it should not throw an error.  
$ rails sever  

# Database creation in app:
1) **Create database.yml from demo_database.yml file.**  
You should fill user name in development section. Password could be empty. It depends on your setup...
2) **Create file option.yml and copy and paste it from Master on Github.**
3) **In Database panel in RubyMine you click on "+" icon and add New database.**
database name: someName@localhost  
host: localhost  
user: foo  
port: XXXX  
url: is generated automatically  
4) **Create database:**
$ rails db:create
5) **Next, migrate it:**
$ rake db:seed  
$ rake db:dev_seed  
$ rails db:migrate  

_**Note for Database initialization Error FATAL:**_ Role "postgres" does not exist (PG::ConnectionBad) Traceback (most recent call last): You can resolve it with Refresh database (click on Recycle icon).
# TESTS:
## How to run the test suite:
Finally, run the test suite to verify that everything is working correctly:  
$ rails test


# Version control on Github:
- Create new repository on Github (without readme a .gitignore)
- Terminal:  
$ git init    
$ git add -A  
$ git commit -m “Initial commit for Gitub”  
_Sets the new remote:_  
$ git remote add origin https://github.com/LukVik/db.git  
_Verifies the new remote URL_  
$ git remote -v  
$ git push origin main  

_**Note:**_ error: failed to push some refs to 'https://github.com/LukVik/db.git'  
$ git push origin master

_**HELP:**_ https://docs.github.com/en/github/importing-your-projects-to-github/importing-source-code-to-github/adding-an-existing-project-to-github-using-the-command-line

# DEPLOY on HEROKU
$ heroku  
If command not found:  
### Install CLI:  
https://devcenter.heroku.com/articles/heroku-cli    
$ brew tap heroku/brew && brew install heroku  
$ heroku  
$ heroku login  

_**Note:**_ you should have created Heroku account in via Authenticator 

### Create remote test server
$ heroku create

### Clone the repository
Use Git to clone *mysterious-temple-91819's source code to your local machine.  
*some_heroku_remote_path

$ heroku git:clone -a some_heroku_remote_path  
$ cd some_heroku_remote_path  

### Deploy your changes  
Make some changes to the code you just cloned and deploy them to Heroku using Git.

$ git add .  
$ git commit -am "make it better"  
$ git push heroku master  
$ heroku run rake db:schema:load

### Send data to Github...
$ git add -A  
$ git commit -m "App to deploy"
$ git push
