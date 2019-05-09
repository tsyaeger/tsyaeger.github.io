---
layout: post
title:      "Postgres Basics"
date:       2019-05-09 03:25:16 +0000
permalink:  postgres_basics
---


Sqlite is the Rails default db and it certainly does the job, but if you want to build a scalable, secure, and extremely stable application or if you want to host your app on Heroku, you’ll want to use Postgres. 

To do so, it is best to create your project configured with psql from the start.

First install [Postgres](http://www.postgresqltutorial.com/install-postgresql/) using ```sudo apt-get install postgresql postgresql-contrib libpq-dev``` and then install the pg gem so that your Postgres db can communicate with Ruby:
```gem install pg``` 

Next, create your Rails app by explicitly setting your db type: ```rails new <myapp> —database=postgresql```

If you open your project you can check out the database.yml file in config. This will work as is, but you have several config options — setting username and password for instance.

Optional: 
Create a username: ```-u postgres createuser -s <username>```, enter Postgres: ```-u postgres psql```, and create a password: ```postgres=# \password cool_user```

Next, you'll generate your routes, models, and controllers as usual, and then create the dbs using
```rake db:create```
OR
```rake db:setup```
and then migrate them with ```rails db:migrate```

If you want to interface directly with the database and you have not added a username or password you can access your db through the CLI using:

```psql -U postgres```

You can then navigate through your dbs using these CLI commands:                                                                                                        
```\l``` list all of your databases enter                                                                                                                                                                  
```\c <dbname>``` to change into a db                                                                                                                                         
```\dn``` list schemas                                                                                                                                                                                                   
```\di``` list indexes
```\dt``` to view tables                                                                                                                                                                                                 
```\q``` to quit                                                                                                                                                                                                                     

Once you’ve entered your database using ```\c```, you can run all of your standard SQL queries. Different db types (sqlite, mysql, etc.) have minor differences in syntax, but they are all well documented.

Now you're off and running!

This is a terrific resource for Postgres queries: https://www.tutorialspoint.com/postgresql/postgresql_select_query.htm
