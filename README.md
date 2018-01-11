# MemCachier Rails Heroku Tutorial App

This is an example Rails application that demonstrates the use of
caching using the [MemCachier
addon](http://addons.heroku.com/memcachier) on Heroku. This example is
written with Rails 5.1.

You can read the full text of the Heroku Dev Center article
[here](https://devcenter.heroku.com/articles/building-a-rails-3-application-with-memcache).

You can see this app in action on Heroku
[here](https://memcachier-examples-rails5.herokuapp.com/).

## Deploy to Heroku

You can deploy this app yourself to Heroku to play with.

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Setup MemCachier

Setting up MemCachier to work in Rails is very easy. You need to make
changes to Gemfile, production.rb, and any app code that you want
cached. These changes are covered in detail below.

### Gemfile

MemCachier has been tested with the [dalli memcache
client](https://github.com/mperham/dalli). Add the following gems to
your Gemfile:

```.ruby
gem 'memcachier'
gem 'dalli'
```

Then run `bundle install` as usual.

Note that the `memcachier` gem simply sets the appropriate environment
variables for Dalli. You can also do this manually in your
production.rb file if you prefer:

```.ruby
ENV["MEMCACHE_SERVERS"] = ENV["MEMCACHIER_SERVERS"]
ENV["MEMCACHE_USERNAME"] = ENV["MEMCACHIER_USERNAME"]
ENV["MEMCACHE_PASSWORD"] = ENV["MEMCACHIER_PASSWORD"]
```

Alternatively, you can pass these options to config.cache_store (also
in production.rb):

```.ruby
config.cache_store = :dalli_store, ENV["MEMCACHIER_SERVERS"],
                    {:username => ENV["MEMCACHIER_USERNAME"],
                     :password => ENV["MEMCACHIER_PASSWORD"]}
```

### production.rb

Ensure that the following configuration option is set in production.rb:

```.ruby
config.cache_store = :dalli_store
```

## Using MemCachier

In your application, use `Rails.cache` methods to access MemCachier.
A list of methods is available
[here](http://api.rubyonrails.org/classes/ActiveSupport/Cache/Store.html).
All the built-in Rails caching tools will work, too.

## Get involved!

We are happy to receive bug reports, fixes, documentation enhancements,
and other improvements.

Please report bugs via the
[github issue tracker](http://github.com/memcachier/examples-rails-heroku/issues).

Master [git repository](http://github.com/memcachier/examples-rails-heroku):

* `git clone git://github.com/memcachier/examples-rails-heroku.git`

## Licensing

This library is BSD-licensed.
