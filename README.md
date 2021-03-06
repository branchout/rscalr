Rscalr
======

Ruby Scalr API implementation. 

Desciption
----------

Rscalr allows your Ops team to build on top of the Scalr API using Ruby. This is particularly beneficial due to the popularity of Chef, a cloud management software suite also written in Ruby.

Rscalr provides both a low-level client implementation, as well as a more user-friendly domain object layer. Here are some brief examples of how to interact with each API mode.

Installation
------------

Rscalr is available on RubyGems so installing it is simply: 

```bash
gem install rscalr
```

Client Usage
------------

```ruby
require 'rscalr'
scalr = Scalr.new({ :key_id => 'your-key-id', :key_secret => 'your-key-secret' })
# list all farms
api_response = scalr.farms_list
# Response objects exted REXML::Document, so you can work with them easily
api_repsonse.pretty_print # Pretty-prints the response XML to a stream ($stdout by default)
```

Domain Model Usage
------------------

```ruby
require 'rscalr'
dashboard = Dashboard.new({ :key_id => 'your-key-id', :key_secret => 'your-key-secret' })
farm = dashboard.get_farm 'my-farm-name'
script = dashboard.get_script 'my-script-name'
# execute the script on all instances in the farm (see Script.rb for all options)
script.execute farm.id
```

Configuration
-------------

If you use this tool a lot from the command line, you can set environment variables that will automagically configure your Scalr or Dashboard instance. The following code sets the relevant parameters:
```bash
export SCALR_API_KEY=your-api-key
export SCALR_API_SECRET=your-api-secret
export SCALR_URL=scalr-api-url, optional, default=https://api.scalr.net
export SCALR_ENV_ID=id-of-desired-environment # optional
export SCALR_CLIENT_VERBOSE=true # Print API calls/responses to stdout, optional, default=false
```

Then just instaniate your client: 
```ruby
scalr = Scalr.new
# or
dash = Dashboard.new
```


Caveats
-------

This client library contains the complete API, but has not been thoroughly tested. The domain model is incomplete and a work in progress. Feel free to submit pull requests and/or suggestions. I am not an experienced Rubyist, so if you see anything in the source that makes you cringe, by all means let me know!
