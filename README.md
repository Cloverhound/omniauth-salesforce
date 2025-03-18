# omniauth-salesforce

[OmniAuth](https://github.com/intridea/omniauth) Strategy for [salesforce.com](salesforce.com).

Note: This is a fork of the [original](https://github.com/richardvanhook/omniauth-salesforce) project and is now the main repository for the omniauth-salesforce gem.

## CSRF Protection

OmniAuth 2.0 includes CSRF protection by default. If you're upgrading from version 1.x, you'll need to ensure your application is configured to handle this. In Rails applications, you might need to add:

```ruby
# config/initializers/omniauth.rb
OmniAuth.config.allowed_request_methods = [:post, :get]
```

Or follow the [OmniAuth CSRF Protection documentation](https://github.com/omniauth/omniauth/wiki/Upgrading-to-2.0) for your specific framework.

## See it in action

[http://omniauth-salesforce-example.herokuapp.com](http://omniauth-salesforce-example.herokuapp.com)

[Source for above app](https://github.com/richardvanhook/omniauth-salesforce-example)

## Basic Usage

```ruby
require "sinatra"
require "omniauth"
require "omniauth-salesforce"

class MyApplication < Sinatra::Base
  use Rack::Session
  use OmniAuth::Builder do
    provider :salesforce, ENV['SALESFORCE_KEY'], ENV['SALESFORCE_SECRET']
  end
end
```

## Including other sites

```ruby
use OmniAuth::Builder do
    provider :salesforce, 
             ENV['SALESFORCE_KEY'], 
             ENV['SALESFORCE_SECRET']
    provider OmniAuth::Strategies::SalesforceSandbox, 
             ENV['SALESFORCE_SANDBOX_KEY'], 
             ENV['SALESFORCE_SANDBOX_SECRET']
    provider OmniAuth::Strategies::SalesforcePreRelease, 
             ENV['SALESFORCE_PRERELEASE_KEY'], 
             ENV['SALESFORCE_PRERELEASE_SECRET']
    provider OmniAuth::Strategies::DatabaseDotCom, 
             ENV['DATABASE_DOT_COM_KEY'], 
             ENV['DATABASE_DOT_COM_SECRET']
end
```

## Resources

* [Article: Digging Deeper into OAuth 2.0 on Force.com](http://wiki.developerforce.com/index.php/Digging_Deeper_into_OAuth_2.0_on_Force.com)
* [OmniAuth 2.0 Documentation](https://github.com/omniauth/omniauth/wiki/Upgrading-to-2.0)
