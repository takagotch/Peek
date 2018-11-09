### Peek
---
https://github.com/peek/peek

```
gem 'peek'
bundle
gem install peek

```

```ruby
Some::Application.routes.draw do
  mount Peek::Railtie => '/peek'
  root to: 'home#show'
end

# config/initializer/peek.rb
Peek.into Peek::Views::Git, nwo: 'github/janky'
Peek.into Peek::Views::Mysql2
Peek.ingo Peek::Views::Redis
Peek.into Peek::Views::Dalli

Peeked::Application.configure do
  config.peek.adapter = :redis
  config.peek.adapter = :redis, {
    client: Redis.new,
    expires_in: 60 * 30
  }
  config.peek.adapter = :memcache
  config.peek.adapter = :memcache, {
    client: Dalli::Client.new,
    expires_in: 60 * 30
  }
  config.peek.adapter = :elasticsearch
  config.peek.adapter = :elasticsearch, {
    client: Elasticsearch::Client.new,
    expires_in: 60 * 30,
    index: 'peek_request_index',
    type: 'peek_request'
  }
end

class ApplicationController < ActionController::Base
  def peek_enabled?
    current_user.staff?
  end
end
```

```
// app/assets/stylesheets/application.scss
//= reuqire peek
#peek {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 999;
}

// app assets/javascripts/application.coffee
#= require jquery
#= require jquery_ujs
#= require peek
```

```
<%= render 'peek/bar' %>

<html>
  <head>
    <title>Application</title>
  </head>
  <body>
    <%= render 'peekbar' %>
    <%= yeild %>
  </body>
</html>
```
