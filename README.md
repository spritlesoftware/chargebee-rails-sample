# Chargebee-rails-sample

Sample rails app built using Chargebee rails subscriptions gem (https://rubygems.org/gems/chargebee-rails-subscriptions)

# Getting Started

  * **Fork and clone the app**
  
  * **Navigate to the *chargebee-rails-sample* folder**
  
  * **Bundle Install**
  
  ```zsh
      
  $ bundle install
    
  ```
  
  * **Migrate the necessary tables**
  
  ```zsh
  
  $ rake db:setup
  
  ```
  
# Setting up the Chargebee Environment

  * **Setup your CHARGEBEE_SITE and CHARGEBEE_API_KEY values in .env file**
  
  ```env
  CHARGEBEE_SITE=your_site_name
  
  CHARGEBEE_API_KEY=your_chargebee_api_key
  ```
  
  * **Sync Plans**
   
  ```zsh
  
  $ rake chargebee_rails:sync_plans
  
  ```
  
  This would sync plans from your chargebee web to the application.
  
  * **Set Default Plan Id**
  
  Once the Plans in Chargebee Web are in-sync with the application, you have to configure the default-plan-id in config/initializers/charegbee_rails.rb file.
  
  ```ruby
  
  # This will be the default plan when a subscription is not provided with one
  # make sure that this plan exists in your active record model
  
  config.default_plan_id = 'default-plan-id'
  
  ```
  
  This would be the "id" of the Plan in Chargebee that you want customers onboarding the application without card details (like a trial experience) to be subscribed to.
  
  **Note**: *Make sure that the default-plan-id is the id of a Plan in Chargebee with trial period.*
  
# Creating a subscription

  * **Open rails console**
  
  ```ruby
  
  customer = Customer.new(first_name: "Test", last_name: "User", email: "test@example.com", phone: "1234556789", company: "New Company")
  
  customer.subscribe
  
  ```
  
  This would create a subscription for the customer in trial status with the default-plan-id the was configured in config/initializers/chargebee_rails.rb
  
# Running the app

 * **Using other payment gateways** 
 
 You could configure Stripe/Braintree Payment Gateways with chargebee and their api_keys with the application to checkout new subscriptions with Stripe/Braintree Payment Gateway.

 In the application provide the values for specific configuration in *.env* file
  
 ```env
 BRAINTREE_MERCHANT_ID='merchant-id'
 
 BRAINTREE_PUB_KEY='braintree-public-key'
 
 BRAINTREE_PRV_KEY='braintree-private-key'
 
 STRIPE_PUBLISHABLE_KEY='stripe-publishable-key'
 ```

 * **Start the server**
 
 ```zsh
 
 $ rails s
 
 ```
 
