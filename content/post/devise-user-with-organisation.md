+++
Categories = ["ruby"]
Description = ""
Tags = ["ruby", "devise"]
date = "2016-09-16T14:41:32+12:00"
menu = "main"
title = "Devise—User With Organisation"

+++

Devise is a great tool to get up and running with user authentication. However, you can get quite stuck. Here's a walkthrough in creating users that belong to an organisation.

In `gemfile.rb`:

```rb
gem 'devise'
gem 'letter_opener'
```

In bash:

```
$ rails g devise:install
$ rails g devise User
$ rails g migration CreateOrganisations name:string
$ rails g migration AddOrganisationToUser organisation:belongs_to
$ rake db:migrate
```

In `config/environments/development.rb`:

```rb
config.action_mailer.delivery_method = :letter_opener
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

And other setting up fluff...

Anyhow, the key thing is how do I sign up when my user depends on belonging to an organisation?

`user.rb`:

```rb
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :trackable, :validatable, :confirmable

  belongs_to :organisation
  has_many :projects
  accepts_nested_attributes_for :organisation

end
```

`views/devise/registrations/new.html.slim`:

```rb
h2
  | Sign up
= form_for(resource, as: resource_name, url: registration_path(resource_name)) do |f|
  - resource.organisation = Organisation.new
  = devise_error_messages!

  .field
    = f.label :email
    br
    = f.email_field :email, autofocus: true

  = f.fields_for :organisation do |of|
    .field
      = of.label :name
      br
      = of.text_field :name

  .field
    = f.label :password
    br
    = f.password_field :password, autocomplete: "off"

  .field
    = f.label :password_confirmation
    br
    = f.password_field :password_confirmation, autocomplete: "off"

  .actions
    = f.submit "Sign up"

= render "devise/shared/links"
```

`registrations_controller.rb` (shortened for important parts):

```rb
class Users::RegistrationsController < Devise::RegistrationsController
  before_action :configure_sign_up_params, only: [:create]

  # POST /resource
  def create
    super
  end

  protected

  # If you have extra params to permit, append them to the sanitizer.
  def configure_sign_up_params
    devise_parameter_sanitizer.permit(:sign_up, keys: [:email, :password, :password_confirmation, organisation_attributes: [:name]])
  end

end
```


