# Ruby On Rails
[Official Guides](https://guides.rubyonrails.org/)

Ruby on Rails, or Rails, is a server-side web application framework written in [[Ruby]] under the MIT License. Rails is a model–view–controller (MVC) framework, providing default structures for a database, a web service, and web pages. It encourages and facilitates the use of web standards such as JSON or XML for data transfer and HTML, CSS and JavaScript for user interfacing. In addition to MVC, Rails emphasizes the use of other well-known software engineering patterns and paradigms, including convention over configuration (CoC), don't repeat yourself (DRY), and the active record pattern.

Ruby on Rails' emergence in 2005 greatly influenced web app development, through innovative features such as seamless database table creations, migrations, and scaffolding of views to enable rapid application development. Ruby on Rails' influence on other web frameworks remains apparent today, with many frameworks in other languages borrowing its ideas, including Django in Python, Catalyst in Perl, Laravel, CakePHP and Yii in PHP, Grails in Groovy, Phoenix in Elixir, Play in Scala, and Sails.js in Node.js.

## CLI
We can make use from the CLI to generate a project or modules to make our life easyer. (Similar to what we can do in other frameworks like React, Angular, ...)

To create a new project:
```
rails new <Name>
```

To start the server:
```
rails s
```

## Application.html.erb
Here we keep the structure of our app seperate from the changing content represented by: **<%= yield %>**.

Everything that doesn't change from page to page in our application can be in here:

-   metadata
-   styling
-   partials
-   ...

## Partial
We can create other html blocks, or _partials_, by creating a new file under views using the pattern:
```
*_<blockName>.html.erb*
```

We can insert this block like this:
```
<%= render '<pathToBlock>/<blockName>' %>
```

Notice the leading underscore is left out of the block we insert.

## New pages
As usual a new page needs:

-   **View**: viewName.html.erb in views folder
-   **Controller**: controllerName_controller.rb in controllers folder
-   **Routing**: routes.rb in config folder

We can do this manually, but this CLI command will do this for us:
```
rails controller home index 
```

## Application helper
Instead of using javascript to check which page is active we can move this logic to rails using **is_active** in _application_helper.rb_:
```
def is_active(action)       
	params[:action] == action ? "active" : nil        
end
```

In the list items in our header this logic can be applied like this:
```
<li class="nav-item <%=is_active('index')%>">
	<%= link_to 'Home', root_path, class:"nav-link" %>
</li>
```

## Scaffold
We use the following CLI command to create a scaffold in _'db/migrate'_:
```
rails g scaffold friends first_name:string last_name:string email:string phone:string twitter:string
```

To create the schema from this scaffold we use this command:
```
rails db:migrate
```

This will not only create a database, but also fully functional CRUD pages to create , update or view entries in _'views/friends'_. This includes even an .scss we deleted in this case because we want to add our own stylign with bootstrap.

## Flash messages
Whenever something goes wrong with CRUD transactions rails will generate messages. To display these messages it needs some placeholders:
```
<%= notice %>
<%= alert %>
```

We can put these anywhere we might need them, so creating a partial we can render anywhere is a good practice.

## Devise
To add the gem go to [Ruby Gems](https://rubygems.org/) and look for devise. You can easily copy the gemfile code with 'copy to clipboard' and pasting it in the project Gemfile.  
In the console we use the following command to have the gem installed:
```
bundle install
```

We can find the devise [README](https://github.com/heartcombo/devise) for more information on how to use it.

We will find that we also need to enter the following command in the console:
```
rails generate devise:install
```

Notice that the console will output more instructions:

-   To configure an Action Mailer, to send people a password when they lost it and similar funtionality.

In _'config/evironments/development.rb'_ and _'config/evironments/production.rb'_:
```
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

-   Make sure we have a root page
-   Make sure we have flash messages like 'notice' and 'alert'.
-   Create devise views.

To create Devise views enter the following in the console:
```
rails g devise:views
```

Devise will also need a _'scaffold'_ (or database model) for users, which we can generate with:
```
rails generate devise user
```

To create the schema from this scaffold we use the same command as before:
```
rails db:migrate
```

We can use the following handle to only display certain html code when the user is logged in by using _'if'_ statements:
```
user_signed_in?
```

## Associations
[Official Guide: Associations](https://guides.rubyonrails.org/association_basics.html)

In the _models_ folder we make these associations:

-   **friend.rb**: belongs_to :user
-   **user.rb**: has_many :friends

We also want to add a user id to our friends table so our schema keeps track of who the 'friends' belong to. For this we enter the following in our console:
```
rails g migration add_user_id_to_friends user_id:integer:index
```

And after a migration we use the same command as before again:
```
rails db:migrate
```

We also need to add _:user_id_ to the list of trusted parameters in _friends_controller.rb_ and add a hidden field to __form.html.erb_:
```
<div class="field">
	<%= form.number_field :user_id, id: :friend_user_id,
	class:"form-control", value:current_user.id, type: :hidden %>
</div>
```

We can prevent usage of the api by adding the following line to the top of _friends_controller.rb_:
```
before_action :authenticate_user!
```

Likewise we want to prevent users from editing friend records of other users:
```
before_action :correct_user, only: [:edit, :update, :destroy]
```

We define _'correct user'_ like this:
```
def correct_user
    @friend = current_user.friends.find_by(id: params[:id])
    redirect_to friends_path, notice: "Not authorized to edit this entry" if @friend.nil?
end
```

We want to update the _new_ and _create_ methods too:
```
def new
  @friend = current_user.friends.build
end

def create
  @friend = current_user.friends.build(friend_params)
  respond_to do |format|
    if @friend.save
      format.html { redirect_to @friend, notice: 'Friend was successfully created.' }
      format.json { render :show, status: :created, location: @friend }
    else
      format.html { render :new }
      format.json { render json: @friend.errors, status: :unprocessable_entity }
    end
  end
end
```

And finally we need to update the querry to only show friends with the right user id if we don't want other people to see the friends from other users.

```
def index
	@friends = Friend.where(:user_id => current_user.id)
end
```

## Custom dialog
For a custom dialog add the following to _'application.js'_:
```
import Rails from "@rails/ujs";
Rails.confirm = function(message, element) {
  let $element = $(element)
  let $dialog = $('#confirmation-modal')
  let $content = $dialog.find('#modal-content')
  let $ok = $dialog.find('#ok-button')
  $content.text(message)
  $ok.click(function(event) {
      event.preventDefault()
      $dialog.modal("hide")
      let old = Rails.confirm
      Rails.confirm = function() { return true }
      $element.get(0).click()
      Rails.confirm = old
    })
  $dialog.modal("show")
  return false;
}
```

And some dialog to your _'application.html.erb'_:
```
<div class="modal fade" id="confirmation-modal" tabindex="-1" role="dialog">
  <div class="modal-dialog modal-dialog-centered modal-sm" role="document">
    <div class="modal-content">
      <div class="modal-body">
        <span id="modal-content"></span>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-sm btn-secondary" data-dismiss="modal">
        	<i class="fa fa-times-circle"></i> Cancel
        </button>
        <button type="button" class="btn btn-sm btn-primary" id='ok-button'>
        	<i class="fa fa-check"></i> Continue
        </button>
      </div>
    </div>
  </div>
</div>
```

## Favicon
To add a favicon we add the file to the _'assets/images'_ folder and simply add the following line to the head in _'application.html.erb'_:

```
<%= favicon_link_tag asset_path('image-name.png') %>
```

## Custom error pages
We can simply find the error pages in the _'public'_ folder and edit them to our liking.

## Hosting an application on Heroku
-   Make sure we are using a solid database like PostgreSQL for the production environment instead of sqlite3.
    
-   Install Heroku toolbelt
    
-   Login to Heroku:
    
    heroku login
    
-   Create an application on Heroku:
    
    heroku create heroku rename name
    
-   Add SSL protection to the project:
    
    heroku keys:add
    
-   Push the application to heroku:
    
    git push heroku master
    
-   Migrate the database:
    
    heroku run rails db:migrate
	
	
	---
	#Ruby