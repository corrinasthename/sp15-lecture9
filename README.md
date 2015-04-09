Lecture 9: Idea to App Part 2
=====

This weeks lecture we will add administrative capabilities to the App from last week.

Initial app - https://github.com/rails-decal/lecture8

```ruby
# Edit ApplicationController to add name parameter.
# Configure devise.rb
# Create buttons on the top right
rake db:migrate

annotate # Generates helpful schema info in model files
```
Step 1 - https://github.com/rails-decal/sp15-lecture9/commit/229e70c7dc0d7f6f9f9d546e42653943cb77cd38


```ruby
rails generate devise:views users # To add name input to views
```
Step 2 - https://github.com/rails-decal/sp15-lecture9/commit/9ca01fcd7b4ec2972dbd41a40556389220ca6fcc


```ruby
# Add cancancan to Gemfile
bundle install
# Update quits controller
```
Step 3 - https://github.com/rails-decal/sp15-lecture9/commit/d2aab4721690bf1d5cac4031b374f3fb4615a8ce


```ruby
rails g cancan:ability # Create ability.rb
# Add this to ability.rb
class Ability
  include CanCan::Ability

  def initialize(user)
    user ||= User.new
    if user.admin?
      can :manage, :all
    else
      can :read, :all
    end
    alias_action :create, :read, :update, :destroy, to: :crud
    can :crud, Quit, user_id: user.id
  end
end
```
Step 4 - https://github.com/rails-decal/sp15-lecture9/commit/bb133cb64aead14ee01d6f186087edc38fa14435

```ruby
rails g migration AddAdminToUsers admin:true
```
Step 5 - https://github.com/rails-decal/sp15-lecture9/commit/2496a6261410fd759872de3cd73054ed188abf8d

