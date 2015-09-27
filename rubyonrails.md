Ruby on rails principle
========================
DRY: Do not repeat yourself
  It allows you to have concise and consistent code which is easy to mantain
  is your code DRY ?

convention over configuration
  only specify the unconventional aspects
  use the sensible defaults used by the rails(follow the convention what rails said, don't try to be smart)
  Follow the best practices (Opinionated)

MVC architecture rails use
============================
Model: Data structue, Object oriented approach design
Views: HTML / CSS / Javascripts
Controller: Listen and process user events, make decision based on 

Rails called the Models, views and controller as
Model: Active Record
Views: ActionView
Controller: ActionController

Action pack: Action view + Action controller grouped together

configuring unix 
====================
sudo vim .bashrc
PS1="\u$ "
export PATH=$PATH:/home/nix10

Install ruby
============
linux has already installed 
1.8 is the dead project
2.x.x series is the stable on

ruby version manager
==================
Rvm => Less popular
rbenv => More popular

installing rbenv version manager
------------------------------------

$ sudo apt-get install git-core curl zlib1g-dev build-essential \
libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 \
libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev #This install dependencies

$ sudo git clone git://github.com/sstephenson/rbenv.git .rbenv #install it from the source code 
$ sudo echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc #adding path of rubyenv to $PATH varible
$ sudo echo 'eval "$(rbenv init -)"' >> ~/.bashrc #used to initilize the environment
$ sudo git clone git://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build #ruby-build install from source
$ sudo echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
$ sudo echo ' source ~/.bashrc' >> ~/.bash_profile #load the configuration for every subshell as well
$ sudo source ~/.bashrc  # execute the changes
 
$ sudo which rbenv # verify the rbenv location
$ sudo cd /home/$USER/.rbenv/plugins
$ sudo pull #pull the changes of ruby plugins, 


install different version of ruby using rbenv
---------------------------------------------
```$ rbenv install 2.2.2
   $ rbenv install 1.8``` #do not use sudo, doesen't work in my case

these ruby version are kept under the ~/home/$USER/.rbenv/ directory

switching the new version of installed ruby
--------------------------------------------
$ rbenv rehash #always, do this, this will ensure when the new ruby packages are installed, some gems need to be loaded into the shell, this will provide the command options of those gmes, so **very very important**
$ rbenv global 2.2.2 #change the global version of ruby

prevent the gems to generate the local documentation of each install
---------------------------------------------------------------------
$ sudo echo "gem: --no-document" > ~/.gemrc


install javascript runtime, as rails features assest pipeline depends on javascript runtime
---------------------------
$ sudo add-apt-repository ppa:chris-lea/node.js
$ sudo apt-get update
$ sudo apt-get install nodejs

install database
----------------
Rails use sqlite as a default database, which is fine for development, but for production we need to use mysql or postgresql

install msyql
----------------
$ sudo apt-get install mysql-server mysql-client libmysqlclient-dev

install msyql2 gem
----------------------
gem install msyql2
Install gems critical to Rails development, e.g.
----------------------------------------------------
$ sudo gem install bundler foreman pg rails thin --no-rdoc --no-ri



rubygem
-------
rubygem is a package manager just like pip for python to  install and manage rubygems(collection of rubycode)
$ sudo apt-get install gem
$ sudo gem -v # display the gem (ruby gems package mangaer version)
$ which gem # print the location of gem manager
$ sudo gem update --system #update the gem manager to latest version
$ gem list #list all the install gems of the development server just like pip freeze of python
$ gem --help #display help how to work with ruby gems
$ ##rubygems.org## is the place where all people push up their gems, central repository just like pypi


installing rails
-----------------
the above steps complete the installation of ruby and database, and ruby gem manager
$ gem install bundler #helps the rails to load right rubygems
$ bundle -v #display the bundler version
$ which bundle # display the location of bundle
$ gem install rails --no-ri --no-rdoc --version 4.0.0  #this will install rails and escape the ri and rdoc documentation files in our machine

web server
-------------
lot of web server there
1. apache for production
2. nginx for production
3. webbrick for development

database configuration for mysql
----------------------------------
open config/database.yml file and set your root password and comment the database,


rails controller
-------------------
$  rails generate controller demo index #here, demo is the controller name and index is the view, all the arguments followed by first arguments will be the view
note: methods defined inside the <name>_controller are also called actions, index will be the action
note: rails controller are just like the django apps

rails file structure
----------------------
app folder:
  concerns folder: exist in models, and controller, the code in this folder is used to share between the model and controllers
  helper folder: contain code that help us with our view
  mailer folder: code to send email
  assets folder: images, javascript and style sheet

bin folder: consist of binary files
  bundle
  rails
  rake

config folder: configuration file for our app
  database.yml: configuration for database
  application.rb: configuration for application for whole
  environment.rb: configuration for environment (dev,prod, test)
  environments folder: contain configuration for different environment
    development.rb => for development code
    configuration.rb => for configuration code
    test.rb => for test code
  Initilizer folder: contain the scripts, for initilization when application launches
  locales folder: for internationalization 

config.ru => configuration files for rack based app, we don't need to open or edit it

db folder: for migrations
Gemfile
Gemfile.lock

lib folder: contain different libraries folder
log folder: logging information

public folder: This folder is public, it is public 
README.rdoc : Documentation of application

test folder: for testing code

tmp directory: for temprorary files   

vendor dir: contain the third party folder

code editor
------------
I choose sublime text 3, fast, and lightweight
should have, 
color hightligting
code completion
auto indent
searchability
support plugins and themes


creating a project CMS
-------------------------
$ mkdir workspace #I manage my projects in workspace directory, some people use site directory
$ cd workspace
$ mkdir simple_cms
$ cd simple_cms 
$ rails new . -d msyql #remember (.) install the files in current directory, and use mysql database as backend, rails has 3 database builtin supported (sqlite, msyql,  postgresl), by having support of plugin we can also use other database like (oracle, ibm_db, sqlserver, frontbase), we can find the plugins in rubygem.org website
 #simple simple_cms will be the root of the rails application

what is bundler
-------------------
Bundler are seperate gems from rails, can be used outside of rails, but rails is going to depend of bundler to manage, see more info of bundler in http://bundler.io
Two files that the bundler concerns on our rails application
1. Gemfile
2. Gemfile.lock => create the tree structue of dependencis of gems, by looking from Gemfile
we will not edit Gemfile.lock, this will be created by the bundler, we will edit the Gemfile according to our requirements

$ bundle install #This will read the Gemfile and create the tree structure of dependencies in Gemfile.lock and install all the dependencies, if you changes or want to test with new version of gem, edit the Gemfile and run the `bundle install` command

accessing project in rails
----------------------------
$ rails server #start the webserver which server the rails app
$ rails s #Shortcut for rails server


rails routing
-----------------
Basic types of route
1. simple route => `get "demo/index"` which is equals to  
`match "demo/index", :to => "demo#index", :via=>"get"`

2. default route: below is the default route pattern
  :controller/:action/:id
example, if /student/edit/2/ comes, this must go to StudentController , edit action (remember, in controller context methods are called action)

in code
`match ':controller/(:action(/:id/))', :via =>:get`

we can also specify the format of the data in routes as well, as
`match ':controller(/:action(/:id(.:format))), :via => :get`  

3. Root route: When we go to the root of the application, there is nothing to match
in code
` root :to => "demo#index"`
the above code equivalent to  `root "demo#index"`  in shortform


rendering templates
----------------------
while rendering templates, the request will be received by the web server, and check for the files, if the files exist in **public** directory the static files 
are serverd from this public_dir without going to the rails framework, if the file doesn't exist in public_dir, the request is received by the routes(routes.rb) and 
match the pattern, if the pattern matches, the request is forwared to the specified controller ( example, if request is **/student/test/)**, the request is forwarded
to the **student_controller** and to **test** action of the **student_controller**, after receiving the request by the controller/action, then the action will load the 
required template defined in the action body as 

```
def test()
  render('test') #This will load the index.html.erb template from **views/student/** directory, you should create that test.html.erb template, this choice is best
  #render(:template # ("demo/test") #equivalent to above code
  #render("demo/test")#same code as of the first line
end
```
in rails, even if we do not specify the template name in the action **test**, it will load the `index.html.erb` template, because this will satisfy by the default route described in the routes.rb file, if the template doesn't exist it will throw 404.html


redirecting action
-----------------------
what is redirect in rails:
  redirect sends the request to the different controller and actions 
  redirect is useful for the password protected page area, if the login successful allow to access page, else redirect to the pages that perform the login process

  redirect code is written in rails action, as example below
  
  ```def other_hello()
      redirect_to(:controller => 'demo', :action=>'index')  
  end```

  ```def other_hello()
      redirect_to("http://google.com") #redirect to google.com website  
  end```

**note**: These are the two things that we are going to do with the action, either we render the template or redirect
  redirect is 302 code

View Temeplates
-------------------
  we can embed the ruby code into the .html.erb (html.embeededruby) code to make our template dynamic code
  eruby tempalting system
  
  code format of embeeded ruby
  -----------------------------
  <% code %> #This will just execute the code
  <%= code %> #This will execute code and output the result of the executed code

instance variable
-------------------
  instance variable: The variable that pass the data from the controller to the view is called instance variable
  @arrary = [1,2,3]

links in rails
-----------------
  To create links in rails, rails gives us a helper method, that is much more powerful 
  Rails gives the link_to helper method to create links, as we put this helper method in this way, this will output the href tag of html `<%= link_to(text, target) %>` 
  so in rails code
  ` <%= link_to("Link to hello", {:action => "hello}) %>` # in this code the controller is not specified because the link goest to the same controller, this link can be
  intepretad as ```<a href="/demo/hello">Link to hello </a>```,
  **Note** if we need to link to the other action of other controller, just use this format `<%= link_to('Link to hello', {:controller => "person", :action =>"profile")

parameters in urls
-------------------
  some times we need to go to particular page, with its id, and this id need to pass to the **link_to** helper method, and this id can be passed in **link_to** methods to the **URL HASH**

  ```{:controller => "demo",
      :action => "hello",
      :id => 1
      :page => 5
      :name => "Manoj" }``` and this code is equivalent to url `/demo/hello/1?page=5&name=Manoj`
    
  To access these parameters, when the request comes in, rails give us a special method calls **params**, params return the Hash that contain all the GET and POST variables that were sent into the request, The hash return is not a regular hash, This is the **HashWithInDifferentAccess** , this is the special kind of hash, it allows us to reference the hashkey with either symbol or a string, example `hash[:id] and hash["id"` are the same so it called **hashwithindifferentaccess**, in normal ruby code it is different and have different meaning.

so to pass the variables to url is just use `<p> Link with params value </p>
`<%= link_to("Link to index", {:action => "index", :id => 1, :page => 12, :name => "ramesh"}) %>` which equivalent to `http://localhost:3000/?id=1&name=ramesh&page=12`
so the variables in the urls and its value can be accessible in the other views of this controller as well as to controller itself, but always get the value inside the controller using params method, as this is the rails convention, to get the variable value in the index action of the demo controller

  ```
    def index()
      @id = params["id"].to_i
      @page = params[:page].to_i
      @name = params["name"].to_i
    end```
while troubleshooting the problems, some times we need to inspect the variables value of the params hash, just do this in template
<%= params.inspect %>

database and migration
===========================

database and migration
-----------------------
common terms
----------------
Database: Set of tables
table: set of columns and rows
in rails 1 model == 1 table
model represent a single concept (a nount) 
Examples, products, persons, these are the rows in the table, as plural form
Column : column are the fields in the database
Rows: Rows are the instance of a class/model
index: data structure in table to increase the lookup speed
foerignkey: table column , the foundation of relational database, example subject_id(rails convention)
schema: structural defination of the database, define table, column, index, everything that make database, importing schema create complete database  

CRUD: Create Read update and Delete/Destroy
------

creating a database in rails
-------------------------------
Rails has the command line features, to create the database, but it is sometimes buggy, as I recommend to create the database from the mysql
some mysql commands
-------------------
`show databases`
`create database <database_name>`
`use database_name`
`drop DATABASE db_name`

create a new mysql user that has permission to our database
`GRANT ALL PRIVILEGES ON db_name.* TO 'username'@'localhost' IDENTIFIED BY 'password'`
`SHOW GRANTS FOR  'username@localhost';
`mysql -u root -p simple_cms_development` # It directly connects to the simple_cms_development database

configure rails project to connect the database
----------------------------------------------------
we can configure the database by going to config.yml
yml is in the **YAML** format, full form of **YAML** is YAML Ain't Markup Language
yaml is the way of structuring the simple text file, and it is suite to the things like configuration files

before configuring the database in .yml file let us understand the rails environment
rails environment
------------------
  Development environment: suited for while developing the apps in developer machine, we want all the error visible, so that we developer can fix this, these error includes the details description of our code, and we dont' want to expose to public
  production: used when our app goes live, we don't want to error to be visible
  test environment: we will use the test database for testing,
It is also possible in rails to add other environment like staging environment, QA environment as your needs but these are the three default environment in rails

rails has the inbuilt command to create database, but it is sometimes buggy, recommendation is just to create a database 

connection test from rails to mysql
--------------------------------------
`rake db:schema:dump` #This command tells rails to connect to database and export schema to database, this will create the new file schema.rb in the db foder

what is rake
---------------
rake is the simple ruby helper program, it is the ruby implementation of make **ruby implementation of make**, It run scripts known as **tasks**
"rake" == "ruby make"
the rake works by using the rake file implementation, which exist on the root of our application
` rake -T ` #This will return the long list of rake tasks
` rake -T db` # This only list the database tasks
Sometime we need to pass environment variables to rake, so that rake can change its variable and response to the environments, for example
` rake db:schema:dump RAILS_ENV=production`

migrations: migration add tables
---------------------------------
Migration are the set of database instruction, written in ruby code, migrate our database from one state to other state, we can do
create a table, add a column, delete a column, drop a table and much more, migration can have instruction to  move *UP* to new state and
back *down* to previous state

Generating migrations
-----------------------------
Migration are resides in the db by creating migrate directory
`$ rails generate migration DoNothing` #Remember the camel case, actually this change to the snake case to migrate folder

Generating models
--------------------
`rails generate model User` This command will generate the models, this will create
1. db/migrate/timestamp_create_users.rb file #As user is the model name(singular) and users is the table name in migration so plural, model name singular, table name plural that is rails convention
2. app/models/user.rb  model file
3. test/models/user_test.rb
4. test/fixtures/users.yml 


creating the table column from the  db/migrate/timestamp_create_users.rb 
```class CreateUsers < ActiveRecord::Migration
  def up
    create_table :users do |t|

      t.column "first_name", :string
      t.timestamps null: false

    end
  end

  def down
  	drop_table :users
  end

end ```

Table column type
---------------------
binary
boolean
date 
datetime
time
decimal
string =>varchar
text => text
integer => int
float

creating the table using ruby code in rails
==============================================
create_table  "table" do |t|
 t.column  "name", :type, options
 t.type  "name", options
end

table column options 
========================
:limit =>size
:default => value
:null =>true/false
:precision => number
:scale => number 

Now let us written the migration for our users table
--------------------------------------------------------
```
def up
    create_table :users do |t|

      t.column "first_name", :string, :limit => 25
      t.string "last_name", :limit => 25
      t.string "password", :limit => 50, :null => false
      t.string "email", :default => "", :null => false 
      #t.datetime "created_at"
      #t.datetime "updated_at"  #shorthand to t.timestampts
      t.timestamps null: false #covered t.datetime "created_at" and t.datetime "updated_at" this handles automatically


    end
  end```
Here we might wondering why dont we have id fields, as all the column have id created automatically by rails, we only need to specify the id if we don't want to have id column, to supress this just add hash after :users as ` create_table :users, {id => false}`  


ok we have created migration for our User table, let us run this migration
running the migration
-------------------------
just go to the root of the app and run the migrate command
`rake db:migrate`
on running this command, this will create the two tables, called
1. schema_migrations
2. users
in the mysql database, so let us login into the mysql server and query the information
`$ mysql -u simple_cms -p simple_cms_development`
`mysql> use simple_cms_development;`
`mysql> show databases;`
`mysql> show fields from users`
`mysql> show fields from schema_migrations`
ok let us see the schema_migrations table, what the data it has
`mysql> show * from schema_migrations`
the schema_migration has the fields called `version` it will track the migrations and we can use this as an id to track the total migrations, and the version has the value of time stamps when the migrations occoured.

Every time we run our migration the rails dumps our schema to `schema.rb` files and the `schema.rb` files always represent the current state of our database

to downgrade the migrations just run the command
`rake db:migrate VERSION=0` #Remember the CAPS letter don't forget
you can verify this by logging into the mysql database and see the tables, you see that the User table has gone, and there is only one table called `schema_migration`
when you query the data in `schema_migration` there is no any versions, when we do again `rake db:migrate` rails will create the new data

`rake db:migrate status` => Give the status of the migration
 Status   Migration ID    Migration Name
--------------------------------------------------
  down    20150927041714  Do nothing
  down    20150927043124  Create users

here you see the status is down, means no database, to restore you can just run the command
`rake db:migrate VERSION=20150927043124` #Remember the capsVERSIOn and number

running migrations commands
----------------------------
`rake db:migrate VERSION=0`
`rake db:migrate VERSION=20150927043124`
`rake db:migrate:status`
`rake db:migrate up VERSION=20150927043124`
`rake db:migrate down VERSIOn=20150927043124`
`rake db:migrate redo VERSION=20150927043124`
**note**, if we dont specify the version number it will assume the last migration
