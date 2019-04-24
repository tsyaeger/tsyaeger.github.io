---
layout: post
title:      "Your client and API are basically just pen pals"
date:       2019-01-23 21:37:36 -0500
permalink:  your_client_and_api_are_basically_just_pen_pals
---


It’s one thing to have an understanding of react and rails, but it is another to understand how they work together. Maybe you can build a React/Redux frontend and a Rails app, you've used APIs and you understand RESTful principles. But do you know how to make your client and server communicate?

First, your react app and your api are completely distinct entities and the only way that they communicate is by making api calls just like the ones you make to unrelated external apis. They just pass messages to one another using requests and responses.  However, your api and your client have a special relationship—albeit one that you must configure.

The Same-Origin Security Policy forbids access to the api whenever a request comes from an external domain. This is the default api state. By using Cross-Origin Resource Sharing (CORS) you can allow request from specific domains. With this method, when the request is sent, the header includes the Origin of the request. In the response the header includes Access-Control-Allow-Origin, which—if everything is working—will be the exact match of the Origin header in the request. The response may also include Access-Control-Allow-Methods in the header as well, which lists the names of methods that are allowed.

Here are the steps I took to set up my api. (You’ll want to use psql if you plan on pushing it to heroku, otherwise you’re in a world of hurt):                                                                                                                                                                                 
1. Use ```rails new rails5_<app_name_api> —api --database=postgresql```, and cd into the new directory
2. Create the psql db using ```createdb <app_name>_api_development``` and then use ```rails migrate:db```
3. Add a model and corresponding controller
4. Add a seed file to create a few objects and populate the db with them using ```rails db:seed```

And here are the CORS config steps:
1. un-comment ```rack-cors``` in the gem file and then run ```bundle install```
2. In the ```config/initializers/cors.rb``` file un-comment this code:
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
       allow do
        origins '*'
		resource '*',
          headers: :any,
          methods: [:get, :post, :put, :patch, :delete, :options, :head]   
	  end   
	end
					```

In the origins line you can replace ```‘*’``` with the domain that the react app will run in.

For routing I used namespaces api/v1, and nested the controllers like so: controllers/api/v1/some_thing_controller.rb

	```
	namespace :api do
	  namespace :v1 do
	    resources :some_thing
	    resources :another_thing
	  end
	end
	```

To run the api you have to use a different port than what the react app will run on. The port can be specified with      ```-p``` like this:
```rails s -p 3001```. This allows the api to run on the base url ```localhost:3001/api/v1```

In the react app you can create a .env file that creates a variable ```BASE_URL=localhost:3001/api/v1```. This variable can be retrieved and used in the app, itself, and utilized in each api call.

Finally, the controllers need to respond appropriately to the request. There are many ways to do this, but here is one common option:

```
def update
	if @some_thing.update_attributes(some_thing_params)
		render json: {status: 'SUCCESS', message: “some_thing updated", data: @some_thing}, status: :ok
	else
		render json: {status: 'ERROR', message: "unprocessable_entity", data: @some_thing.errors}, 
		status:  :unprocessable_entity
	end
end
```


Once you get this up and running, you’ll want to download postman and add your api [getpostman](https://www.getpostman.com/)
. It will help you ensure that your api is working properly, to properly structure requests, and handle responses.

This is a killer resource for how to use postman: [api-testing-using-postman](https://medium.com/aubergine-solutions/api-testing-using-postman-323670c89f6d. )



