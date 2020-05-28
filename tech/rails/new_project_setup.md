# Nice Rails resources:
- https://guides.rubyonrails.org
- https://www.theodinproject.com/courses/ruby-on-rails
- https://thoughtbot.com/upcase/rails

# New Project Setup:

## Bare Start:
1. `gem install rails`
1. create the bitbucket repo
1. `rails new PROJECTNAME  -d postgresql`
1. do the bare rails new project push to the repo

## Setup the Test Env:
1. see: https://github.com/rspec/rspec-rails
1. delete `test` folder, use only the spec from now on
1. see: https://github.com/thoughtbot/factory_bot_rails
1. create the `spec/factories` folder
1. copy bin/rspec and then run `bundle binstubs bundler --force`
1. optional: https://github.com/travisjeffery/timecop

## Admins CRUD:
1. use `gem "kaminari"`
1. use `gem "bootstrap_form", ">= 4.0.0.alpha1"`
1. `rails g kaminari:views bootstrap4`
1. create the `current_page` method at the admin controller
1. Partial `layouts/_form_record_errors`
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/6a4fe418db05ed8cfb1d7f1867e233eb3c789cd0

## S3 Bucket Setup:
1. Amazon AWS Console (login with: infra.devmaker@gmail.com)
1. Create a bucket and copy the configs from other bucket
1. set the current CORS polycy
    ```
    <?xml version="1.0" encoding="UTF-8"?>
      <CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
      <CORSRule>
          <AllowedOrigin>*</AllowedOrigin>
          <AllowedMethod>GET</AllowedMethod>
          <AllowedMethod>POST</AllowedMethod>
          <AllowedMethod>PUT</AllowedMethod>
          <AllowedHeader>*</AllowedHeader>
      </CORSRule>
    </CORSConfiguration>
    ```
1. create a new IAM user for the project
1. set permission on this project buckets only (https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_examples_s3_rw-bucket.html)
1. Copy ID + Secret and Add them to s3 key at `rails credentials:edit`
1. add the `gem "aws-sdk-s3", "~> 1"`
1. copy the `aws.rb` initializer and update the settings

## Private Admin Area Setup:
1. Create a temporary Admin::Dashboard#index page
    1. `rails g controller Admir/Dashboard index`
1. Add devise: https://github.com/plataformatec/devise#getting-started
    1. follow after install instructions
    1. `root "admin/dashboard#index"`
    1. dont need to generate the views yet
    1. add devise pt-BR translations with the gem: https://github.com/tigrish/devise-i18n
1. Generate de user devise model: `rails generate devise User`
1. create the admin model with a polymorphic has_one relation to user
1. add the polymorphic association
1. Protect the admin Controller:
    1. Create the AdminController
    1. change the Admin::DashboardController
    1. https://bitbucket.org/RudineyFranceschi/cartax/commits/1ad21d0d356d6c975f6fd64c602b7f3d6325ef90

### Add the Bootstrap Template Styles:
1. add `gem "bootstrap_form", ">= 4.0.0.alpha1"`
1. add `gem "jquery-rails"`
1. copy de `package.json` file and run `yarn install`
1. copy the entire `vendor/assets` folder
1. copy the `layout/application.html.erb`
    1. copy `layouts/_flash_messages`
    1. copy/edit `layouts/admin/header`
    1. copy/edit `layouts/admin/menu`
    1. change the `app/assets/images/logo`
1. create the `layout/admin.html.erb`
1. in `assets.rb`
    1. add `admin.css admin.js` to precompiled_assets
    1. add `Rails.application.config.assets.paths << Rails.root.join("vendor", "assets")`
1. copy the `app/assets/stylesheets/admin.css` & `app/assets/javascripts/admin.js`
1. copy the `admin/menu.js`
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/8bb477a00c947eecb04b1b69573076e74e295997/

## Add a Public GQL API:
1. see http://graphql-ruby.org/getting_started
1. add `gem "graphql"`
1. `bin/rails generate graphql:install --schema=PublicSchema`
2. :warning: graphiql-rails has a bug. use version < 1.5 (see: https://github.com/rmosolgo/graphiql-rails/issues/58)
1. Move & Rename genetared `MutationType` & `QueryType` to `PublicMutationType` & `PublicQueryType` at the schema also
1. copy the `GraphqlControllerMixin` controller concern
1. move & change the `GraphqlController` to `Public/GraphqlController`
1. change the route to use the public/grapql controller `post "/graphql", to: "public/graphql#execute"`
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/3e3e9ba360eade4ed89506cdf03937dee7b19e60/

## Mutation to signup an Passenger at the public api:
1. Copy the `ErrorHandlingMutation` mutation mixin
1. Copy the `BaseMutation`
1. Create the `Passenger` model with has_one :user
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/cc5cc8c26f2dec585f25cceeceb39dcead1e4585/
1. create the `passengerSignup` mutation
1. return a public version of the Passenger (`Types::Models::PublicPassengerType`)
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/b1917b2f50bec9f9daea711afa91531d61d29a31/

## Mutation to Login:
1. Add doorkeeper https://github.com/doorkeeper-gem/doorkeeper
1. integrate with devise https://github.com/betterup/devise-doorkeeper
1. Check both `devise.rb` & `doorkeeper.rb` config
1. copy `UserTokenType`
1. copy `graphql/mutations/mixins/handle_login_mutation.rb`
1. Mutation to login ond return a token
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/36ea0bf4d55a8ca880390432b2675dbbe3af5f95/

## Create a Private Passenger API:
1. new graphql route & Schema
1. simple `Me` query returning a `PassengerType`
1. example commit: https://bitbucket.org/RudineyFranceschi/cartax/commits/15d4014c2356bdbc270a3985b78322a60e7d8917/

## Setup Postgis:
1. locally install postgis: `brew install postgis`
1. gem: https://github.com/rgeo/activerecord-postgis-adapter
1. heroku setup: https://devcenter.heroku.com/articles/postgis
1. change rails database config:
    1. https://devcenter.heroku.com/articles/rails-database-connection-behavior
    1. url: <%= ENV.fetch('DATABASE_URL', '').sub(/^postgres/, "postgis") %>
1. example with CheckPoints Table: https://bitbucket.org/RudineyFranceschi/cartax/commits/e13522267b5855f111cc6150cfd8ff0d6d94136e/

## Push Notifications:
1. FCM gem: https://github.com/spacialdb/fcm
1. Copy PushNotification class
1. Copy the Base Notification class

## Heroku Deploy:
1. be sure to have `ruby "2.5"` at Gemfile
1. `heroku apps:create cartax-staging --remote=staging`
1. `heroku buildpacks:add heroku/nodejs`
1. `heroku buildpacks:add heroku/ruby`
1. `heroku config:set BUNDLE_GITLAB__COM=devmaker-ci-cd:THE_SUPER_SECRET_PASSWORD` (if the project uses this gem from the private gitlab repo)
1. `heroku config:set RAILS_ENV=staging -a YYYY-staging`
1. `heroku config:set RAILS_MASTER_KEY=[master.key string] -a YYYY-staging`
1. create a `Procfile` file at root (maybe the first time you create the database you cant have the `release` Procfile line)
    ```
    web: bundle exec puma -C config/puma.rb
    release: bundle exec rake db:migrate
    ```
1. Configure the heroku final url: (at production.rb or staging.rb)
    ```
    Rails.application.routes.default_url_options = {host: "http://YOUR-APP-NAME-HERE.herokuapp.com"}
    config.action_mailer.default_url_options = Rails.application.routes.default_url_options
    config.action_controller.default_url_options = Rails.application.routes.default_url_options
    ```
1. replace the default js_compressor to enable Uglyfier harmony mode: `config.assets.js_compressor = Uglifier.new(harmony: true)`
1. Create a staging rails env and set at the heroku staging app
    1. copy `config/production.rb` and change url
    1. change the `database.yml` to set staging like prod
1. set this to `staging.rb` and `production.rb`:
    1. `config.assets.js_compressor = Uglifier.new(harmony: true)`
1. After the deploy is done:
    1. `heroku run rake db:schema:load -a YYYYYYY`
    1. `heroku run rake db:seed -a YYYYYYY`


# Emails with fancy styles?
1. Consider: https://github.com/TedGoas/Cerberus

# Production Background Jobs Structure
1. Start understanding how Rails ActiveJob works: https://guides.rubyonrails.org/active_job_basics.html
1. Instal redis in your machine (`brew install redis`?)
1. Add (or buy) the `Heroku Redis` addon to your heroku app
1. Add sidekiq and redis gems:
    ```
    gem "redis", "~> 4.0"
    gem "sidekiq"
    ```
1. Run `bundle install`
1. Tell Heroku to start a new process to run `sidekiq` by adding this to `Procfile.dev`:
    ```
    worker: bundle exec sidekiq -e $RAILS_ENV -c 10
    ```
1. Check if you have to pay for this new process at your heroku app
1. Add `config.active_job.queue_adapter = :sidekiq` to `config/application.rb`
1. Add the sidekiq web interface by adding `mount Sidekiq::Web => "/sidekiq"` to `routes.rb`
1. Require a username and password authentication for this ui in production:
    1. add this to the *top* of the `routes.rb`:
    ```
    require 'sidekiq/web'
    Sidekiq::Web.use Rack::Auth::Basic do |username, password|
      ActiveSupport::SecurityUtils.secure_compare(::Digest::SHA256.hexdigest(username), ::Digest::SHA256.hexdigest(ENV["SIDEKIQ_USERNAME"])) &
        ActiveSupport::SecurityUtils.secure_compare(::Digest::SHA256.hexdigest(password), ::Digest::SHA256.hexdigest(ENV["SIDEKIQ_PASSWORD"]))
    end if Rails.env.production?
    ```
# ActionCable Setup (to send notifications to each user using websocket)

1. Add redis gem:
    ```
    gem "redis", "~> 4.0"
    ```
1. Run `bundle install`
1. Create NotificationsChannel (notifications_channel.rb) in app/channels
    ```
    class NotificationsChannel < ApplicationCable::Channel
      def subscribed
        stream_for current_user
      end
    end
    ```
1. Change the class Connection in channels/application_cable/connection.rb:
    ```
    module ApplicationCable
      class Connection < ActionCable::Connection::Base
        identified_by :current_user
    
        def connect
          self.current_user = find_verified_user
          logger.add_tags "ActionCable", current_user.id
        end
    
        protected
    
        def find_verified_user
          puts("verifying")
          verified_user = env["warden"].user || User.find_by(id: access_token&.resource_owner_id)
          verified_user || reject_unauthorized_connection
        end
    
        def access_token
          @access_token ||= Doorkeeper::AccessToken.by_token(
            request.query_parameters[:token]
          )
        end
      end
    end 
    ```  
1. Add the following configuration to the module Pattern in config/application.rb:
    ```
    config.action_cable.disable_request_forgery_protection = true
    ```
## Testing if websocket is working to message user

1. You must have user authentication system and at least one registered user (in our example we name it user1 = User.find(1))
1. Configure the development adapter in `config/cable.yml`:
    ```
    development:
      adapter: redis
      url: <%= ENV.fetch("REDIS_URL") { "redis://localhost:6379/1" } %>
      channel_prefix: {your-project}_development
     ```
     
1. Create a file `test.coffee` on the directory `app/assets/javascripts` and add the following content to it:
    ```
    App.room = App.cable.subscriptions.create "NotificationsChannel",
      connected: ->
        console.log('connected')
      received: (data) ->
        console.log(data['message'])
    ```
1. Add the created `test.coffee` and `cable.js` to the `admin.js`
    ```
    //= require cable.js
    //= require test.coffee
    ```
1. Login with user1 and open the browser console. If it displays "connected", the websocket is working.
1. Run `rails console` in the terminal and try sending a message to the user1
    ```
    ActionCable.server.broadcast_to user1, message: "hello user"
    ```
1. If the response to this command is "1", the message was sent by the websocket. Check if the message "hello user" arrived on the browser console opened earlier.