# Building GuitHubApp with Ruby containing GitHub WebHooks
=========

## Smee
========
to to url: 
   https://smee.io/
click: 
    start new channel
output: 
    https://smee.io/********************

### Instructions:
======
Note: 
    The following steps are slightly different than the "Use the CLI" instructions you'll see in your Smee channel page. You do not need to follow the "Use the Node.js client" or "Using Probot's built-in support" instructions.
Enter in browser Webhook Proxy URL:
    https://smee.io/********************
This page will automatically update as things happen.
Use the CLI in shell:
    $ npm install --global smee-client
Result:
Then the smee command will forward webhooks from smee.io to your local development environment.
    $ smee --url https://smee.io/******************** --path /event_handler --port 3000
    Forwarding https://smee.io/******************** to http://127.0.0.1:3000/event_handler
    Connected https://smee.io/********************

## GitHub App
=========
Go to:
    https://github.com/settings/apps/new
Enter following fields
app name: 
    TutGHApp-set-up-yr-dev-env
homepage url: 
    https://smee.io/********************
webhook url: 
    https://smee.io/********************
webhook secret: 
    xxxxxxxxxxxxxx

## Generate private key for GitHub App
===============
Go to:
    https://github.com/settings/apps/tutghapp-set-up-yr-dev-env
Click button to generate private key which returns
file containing RSA key: 
    tutghapp-set-up-yr-dev-env.2019-01-15.private-key.pem
and response on website: app ID GitHub has assigned to app
    Owned by: @qoolixiloop
    ID: 23726

## add file .env
======
copy/paste the following information 
rsa key 
    from the file ...private-key.pem
ID
    23726
webhooksecret
    xxxxxxxxxxxxxx

## template_server.rb
=========
try to understand the template code

## try to run Sinatra web server
=============
ERROR for gem install bundler because of ownership:

## install a local version of ruby in $HOME:
======
### Install dependencies    
    $ cd $Home
    $ sudo apt-get update 
    $ sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev
### Install rbenv
    $ git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    $ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    $ echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    $ exec $SHELL
### Install ruby-build
    $ git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    $ echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
    $ exec $SHELL
### Install newest version and set it global 
    $ rbenv install 2.6.0
    $ rbenv global 
     system
    $ ruby -v
    ruby 2.5.1p57
    $ which ruby
    /home/benzro/.rbenv/shims/ruby
    $ rbenv global 2.6.0
    $ ruby -v
    ruby 2.6.0p0
### Install gem bundler
    $ gem install bundler
    $ rbenv rehash
    $ rbenv global system

## Install gems for App
=========
    $ cd this_folder
create a .env file
    $ rbenv local 2.6.0
install gems
    $ bundle install

## run Sinatra web server
========    
    $ ruby template_server.rb

## install app on github qoolixiloop account
=========
    https://github.com/settings/apps/tutghapp-set-up-yr-dev-env/installations

### webhook works
=========
This creates an event in Github and the webhook sends a notification 
via Smee webpage to shell with local Smee. 
From there it is sent to shell with Sinatra web server which shows message in 
shell.

### app works
=========
message on both bash shells
Refreshing the browser tab listening to Sinatra shows that the App also works.
It shows an error message, which is fine since no route has been defined in
template_server.rb

### stop both servers
=========
    Ctrl-c
