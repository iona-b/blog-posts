![Cover Image](./cover-image.jpg)

*photo by [@georgie_cobbs](https://unsplash.com/@georgie_cobbs)*

# Params and Rails

Experimenting with creating your first Rails app can be an exciting experience, but one aspect that can be confusing for beginning developers is the idea of params, and how to ensure we have access to the data we need, whether it be information given to us by users, or items that we want to pass behind the scenes. In this post we'll take a look at some different ways in which this can be achieved.

<br>

## What Are Params?

Params are the parameters which are passed to the controller via a GET or POST request, and come from the ActionController::Base. Your application is able to access these params through the ApplicationController. Generally params are comprised of information given to you by your user, for instance through a URL or a form, however we often need access to and control over params in situations where our user hasn't entered any new information.

<br>

## Passing Params

### Passing Params Through the URL

The most simple way in which we get params from a user is through the URL they use. When the user enters, for instance, some_website/users/22, the parameters we have access to will look something like this:

```ruby
<ActionController::Parameters {"controller"=>"users", "action"=>"show", "id"=>"22"} permitted: true>
```

By adding the id "22" to the end of their URL, the user is specifying which profile they'd like to see. As a result, we now have access to this id, and can use it to show the user exactly what they're looking for by using the params[:id] in our UsersController show action. 

```ruby
def show
    @user = User.find(params[:id])
end
```

While useful and necessary, this is a basic example of params, and there are many other ways in which a user can provide information for us to work with. Below we'll examine how to handle data submitted by the user, and how we can pass this data from one view to another.

<br>

### Passing Params Through a Form

The first way of passing params that developers usually become familiar with is through a form. There are several different ways in which you can construct forms, some of which are explored further here: https://dev.to/ionab/what-s-this-formfor-fee .

In this example, we're allowing the user to create a new profile using form_for. 

```ruby
<h2><%= "Create a Profile" %></h2>

<%= form_for @user do |f| %>
    Username: <%=f.text_field :username %><br><br>
    Password: <%=f.password_field :password %><br><br>
    Location: <%=f.text_field :user_location %><br><br>
    <%=f.submit %>
<% end %>
```

Once the user submits their information into the text fields, we need to have access to that data in order to add their profile to our database. Below, we can see the params that we have access to for this purpose:

```ruby
<ActionController::Parameters {"authenticity_token"=>"6Uz75TYfsd5Q5HAkJzZKGl7Vjc4pLPsyFsjsPQZGmorhMYMNM29rD9pfJjWXJ/156fUbz9L8uoBjDoHeRdi56A==", "user"=><ActionController::Parameters {"username"=>"andy", "password"=>"password", "user_location"=>"San Francisco"} permitted: true>, "commit"=>"Create User", "controller"=>"users", "action"=>"create"} permitted: true>
```

All of the information entered by the user is accessible to us, and we can choose to utilise and manipulate it as we wish. In this case, we've taken the extra step of setting up strong params using the following method in our UsersController:

```ruby
    def user_params
        params.require(:user).permit(:username, :password, :user_location)
    end
```

*Strong params are an optional but highly-recommended part of a developer's toolkit. Rather than allowing the user to edit our form and provide us with potentially malicious input, we define what we require (in this case the :user instance), and what we permit (here the :username, :password, and :user_location).*

This method means that we can access the data by calling user_params. For instance, if we wanted to access the username, we could do that like so:

```ruby
user_params["username"]
```

As we're creating a new profile for our user in this example, we'd probably want to pass the params to a create action:

```ruby
def create
    @user = User.new(user_params)
    @user.save
    redirect_to @instructor
end
```

By using params containing the data entered by our user, we're able to add their profile to our database.

<br>

### Passing Params Through a Hidden Field Tag

While it's fairly straightforward to see how we can access data that has been entered through a form, it can be a little more complicated to work out how to pass information between views when we don't have any direct input from the user at that specific moment. For instance, we can imagine that a user has selected certain items from our online store, and is now being asked if they'd like to proceed to the order summary. We need to make sure that the information about the items they've selected is carried over to the new order page, so that they can see what they've chosen before actually finalising anything. It would be annoying for the user to have to re-enter anything, so we can just pass the information they've already given us using a hidden_field_tag, like so:

```ruby
<%= form_for @order do |o| %>
    <%= hidden_field_tag(:item_1, @item[0].id) %>
    <%= hidden_field_tag(:item_2, @item[1].id) %>
    <%= o.submit "Proceed to Order Summary" %>
<% end %>
```

On this page, we have access to an @items array, and we are setting :item_1 and :item_2 to the ids of the first and second elements in that array. Obviously, this is quite a narrow example, as we are only allowing the user to select two items, however this can be expanded depending on the functionality of your application.

<br>

### Passing Params Through a button_to

There are often situations in which we don't have a form, but still need to be able to pass information. One way in which we can do this is by defining params in a button_to, like so:

```ruby
<%= button_to "Place an Order", new_order_path, params: {items: @items}, method: :get %><br>
```

Again, we wouldn't want to the user to have to re-enter information whenever they change page, so we can make sure all of the data goes along with them by setting items: to @items in our params. This means that we can access items in our params in the same way that we would access that data if they had submitted it through a form. Using params with a button_to allows us to determine what data we need and to make sure that we have access to it in the next view.

<br>

### Passing Params Through a link_to

Similarly, we are also able to pass params through a link_to. The syntax is slightly different and doesn't involve us defining params: as we did with button_to, however it passes the information in much the same way. In this example, it will allow us access to the @item.id and @style.id in the next view:

```ruby
<%= link_to @item.name, new_order_path(item_id: @item.id, style_id: @style.id) %><br>
```

While it seems to the user that they are simply clicking a link, we are passing extra information on the back end, allowing our app to run more smoothly, and negating the need for the user to re-enter any information.

<br>

### Which of These Options Works Best?

Depending on the specific needs of your app, any one of these different methods can be useful in terms of taking data from your user, and having access to that information. You may want to use a hidden_field_tag if your user is submitting a form, and your application requires that you pass on additional information. Passing data through a link_to or a button_to allows you to carry over params in situations where your user isn't entering any new information, and you just need to carry data over behind the scenes. 

## Sources

1. "[Action Controller Parameters](https://api.rubyonrails.org/classes/ActionController/Parameters.html)", API, Accessed September 8 2020
2. "[hidden_field_tag](https://apidock.com/rails/ActionView/Helpers/FormTagHelper/hidden_field_tag)", API, Accessed September 8 2020
