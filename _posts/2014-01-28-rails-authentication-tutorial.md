---
layout: post
title: "Rails Authentication Tutorial"
description: ""
category: 
tags: []
---
{% include JB/setup %}

Basic Authentication

`rails g controller users new`
`rails g model user email:string password_hash:string password_salt:string`
`rake db:migrate`

## Create a new user (A way to sign up)

	class UsersController < ApplicationController
		def new
			@user = User.new
		end

		def create
			@user = User.new(params[:user])
			if @user.save
				redirect_to root_url, :notice => "Signed up!"
			else
				render "new"
			end
		end
	end
### Create form

### Change Routes file
create the alias "sign_up" for "users#new" action
set the site root to go to "users#new"
give the resource access

	get "sign_up" => "users#new", :as => "sign_up"
	root :to => "users#new"
	resources :users

### Edit User Model
	class User < ActiveRecord::Base
		attr_accessor :password

		validates_confirmation_of :password
		validates_presence_of :password, :on => :create
		validates_presence_of :email
		validates_uniqueness_of :email, :on => :create, :message => "email must be unique!"
	end

### Gemfile

	gem "bcrypt-ruby"
	
then be sure to run

	bundle install

### Edit User Model

	class User < ActiveRecord::Base
		attr_accessor :password
		before_save :encrypt_password

		validates_confirmation_of :password
		validates_presence_of :password, :on => :create
		validates_presence_of :email
		validates_uniqueness_of :email, :on => :create, :message => "email must be unique!"

		def encrypt_password
			if password.present?
				self.password_salt = BCrypt::Engine.generate_salt
				self.password_hash = BCrypt::Engine.hash_secret(password, password_salt)
			end
		end
	end

### Check in console
Create an account
go into console to verify 
	rails dbconsole
	select * from users;

## Next creating the session (a way to login)
Generate a session controller with 'new' action

	rails g controller session new

Inside the new.html.erb in `session`

	GRAB CODE FROM HITHER!
	http://railscasts.com/episodes/250-authentication-from-scratch?autoplay=true

### Edit the routes

	get "log_in" => "sessions#new", :as => "log_in"
	get "sign_up" => "users#new", :as => "sign_up"
	root :to => "users#new"
	resources :users
	resources :sessions

### Sessions controller

Add the create action

	class SessionsController < ApplicationController
		def new
		end

		def create
			user = User.authenticate(params[:email], params[:password])
			if user
				session[:user_id] = user.id
				redirect_to root_url, :notice => "Logged in!"
			else
				flash.now.alert = "Invalid email or password"
				render "new"
			end
		end
	end

### Authenticate
Check that the user exists and his password matches the database

	class User < ActiveRecord::Base
		...

		def self.authenticate(email, password)
		    user = find_by_email(email)
		    if user && user.password_hash == BCrypt::Engine.hash_secret(password, user.password_salt)
		      	user
		    else
		      	nil
		    end
		end

## References
- [http://www.sitepoint.com/rails-userpassword-authentication-from-scratch-part-i/](http://www.sitepoint.com/rails-userpassword-authentication-from-scratch-part-i/)

- [http://railscasts.com/episodes/250-authentication-from-scratch?autoplay=true](http://railscasts.com/episodes/250-authentication-from-scratch?autoplay=true)