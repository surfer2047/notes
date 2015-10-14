ugilifier: This gem will handle the file compresssion for javascripts accets
Gemfile: This is the ruby file
gem 'sqlite3', '>=3.0.0' 
gem 'sqlite3', '~>3.0.0'

>=: Will alwasy install the latest gems
~>: Will always install the update gems [3.0.1, change to minor release, not update to 3.1.0, in rails even minor release can break things]

MVC allows the seperation from the "Domain logic", Domai Logic is also called the business logic from the "Input and presentation logic" 
In the Domainlogic/Business logic it contain the information of Data/MOdel

* In default we have only the one controller which is called **application_controller.rb**
* ```
	def index()
		render text: "Hello world"
	end	




writing actions
============
==============


def index
	render text: "Hello world"
end


writing routes
================
root "application#index"  
Here, application is the controller name and index is the action, function inside application
