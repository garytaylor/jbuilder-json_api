# Jbuilder::JsonApi

JsonAPI assistance for jbuilder

Using jbuilder in your project and want to stick with it, but you want to use the jsonapi format (http://jsonapi.org/format)

Of course you can do it all yourself and if you are just doing basic stuff, its not too hard.
But, it clutters up your views with stuff you aren't really interested in, you just want to focus on the application
that you want to write.

This gem helps you do just that.

Here are some examples of how to use it.

Lets say @product is an active record model and @products is an active record scope that responds to normal
things like :all, :where etc...

## Example 1 a very simply collection of products

```ruby
json.json_api_collection scope: @products do
  json.array! @products do |product|
    json.name product.name
    json.price product.price
  end
end
```

which will output

```json
{
    "data": [
        {
            "id": 1,
            "type": "products",
            "attributes": {
                "name": "My Product",
                "price": 5.99
            }
        }
    ],
    "errors": [],
    "meta": []
}

```
Not too much clutter in the jbuilder file - nice and simple, but lets say you want a bit more control,
for example, you want the "id" to be the "slug" attribute of your model.

## Example 2 - Custom primary key

```ruby
json.json_api_collection scope: @products, primary_key: :slug do
  json.array! @products do |product|
    json.name product.name
    json.price product.price
  end
end
```

which will output

```json
{
    "data": [
        {
            "id": "my_product_slug",
            "type": "products",
            "attributes": {
                "name": "My Product",
                "price": 5.99
            }
        }
    ],
    "errors": [],
    "meta": []
}

```



TODO: Delete this and the text above, and describe your gem

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'jbuilder-json_api'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install jbuilder-json_api

## Usage

TODO: Write usage instructions here

## Development

After checking out the repo, run `bin/setup` to install dependencies. Then, run `bin/console` for an interactive prompt that will allow you to experiment.

To install this gem onto your local machine, run `bundle exec rake install`. To release a new version, update the version number in `version.rb`, and then run `bundle exec rake release` to create a git tag for the version, push git commits and tags, and push the `.gem` file to [rubygems.org](https://rubygems.org).

## Contributing

1. Fork it ( https://github.com/[my-github-username]/jbuilder-json_api/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request
