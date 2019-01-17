# Using github-app-template


## Clone template
git clone https://github.com/github-developer/github-app-template.git


You can use this GitHub App template code as a foundation to create any GitHub App you'd like. You can learn how to configure a template GitHub App by following the "[Setting up your development environment](https://developer.github.com/apps/quickstart-guides/setting-up-your-development-environment/)" quickstart guide on developer.github.com.

## Install

To run the code, make sure you have [Bundler](http://gembundler.com/) installed; then enter `bundle install` on the command line.

## Set environment variables

1. Create a copy of the `.env-example` file called `.env`.
2. Add your GitHub App's private key, app ID, and webhook secret to the `.env` file.

## Run the server

1. Run `ruby template_server.rb` on the command line.
1. View the default Sinatra app at `localhost:3000`.

--------
--------

# Using github-app-template: Building my own GitHub App "tutghapp-set-up-yr-dev-env" with Ruby containing GitHub WebHooks

The steps below are a summary of this tutorial:

    https://developer.github.com/apps/quickstart-guides/setting-up-your-development-environment/

## Smee

Go to url: 

    https://smee.io/  

click:  

     start new channel  
     
output:   

    https://smee.io/********************  

### Instructions:  

Note:  

    The following steps are slightly different than the "Use the CLI" instructions you'll see in your Smee channel page. You do not need to follow the "Use the Node.js client" or "Using Probot's built-in support" instructions.  

Enter in browser Webhook Proxy URL:  

    https://smee.io/********************  
    
> This page will automatically update as things happen.  

Use the CLI in shell:  

    $ npm install --global smee-client  
    
Result:  
Then the smee command will forward webhooks from smee.io to your local development environment.  

    $ smee --url https://smee.io/******************** --path /event_handler --port 3000  
> Forwarding https://smee.io/******************** to http://127.0.0.1:3000/event_handler  
> Connected https://smee.io/********************  

## GitHub App
Go to:  

    https://github.com/settings/apps/new
    
#### Enter following fields  

app name: 

    TutGHApp-set-up-yr-dev-env
    
homepage url: 

    https://smee.io/********************  
    
webhook url: 

    https://smee.io/********************   
    
webhook secret: 

    xxxxxxxxxxxxxx   

## Generate private key for GitHub App
Go to:  

    https://github.com/settings/apps/tutghapp-set-up-yr-dev-env  
    
Click button to generate private key which returns:  

a file containing RSA key: 
* tutghapp-set-up-yr-dev-env.2019-01-15.private-key.pem  

and a response on website: app ID GitHub has assigned to app  
* Owned by: @qoolixiloop  
* ID: ididid  

## add file .env
Copy/paste the following information into file .env.  

rsa key: 
    from the file: ...private-key.pem  

ID:  
    ididid   

webhooksecret: 
    xxxxxxxxxxxxxx   

## Open template_server.rb
Try to understand the template code.

## Try to run Sinatra web server

    $ ruby template_server.rb  
    
if you get following message: 
* ERROR for gem install bundler because of ownership.
* it's because your are running on Ubuntu's system Ruby installation.
* Don't mess around there, just install a new version in your $HOME, by following the steps below.

## Install a local version of ruby in $HOME:
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

    $ cd this_folder  
    
Create an .env file:  

    $ rbenv local 2.6.0  
    
Install gems:  

    $ bundle install  

## Run Sinatra web server
 
    $ ruby template_server.rb  

## Install app on github account

    https://github.com/settings/apps/tutghapp-set-up-yr-dev-env/installations

### Webhook works
This creates an event in Github and the webhook sends a notification via Smee webpage to shell with local Smee. 
From there it is sent to shell with Sinatra web server which shows message in shell.

### App works
Message received on both bash shells.
Refreshing the browser tab listening to Sinatra shows that the App also works.
It shows an error message, which is fine since no route has been defined in template_server.rb

### Stop both servers

    Ctrl-c

