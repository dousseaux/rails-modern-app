# Modern Rails App

The goal of this project is to showcase a simple modern rails app for those who are used with the old good rails (like I was).

This project features Rails 6 with: react, webpack and graphQL.

Starting:

```
rails new modern-app -d mysql --skip-action-mailbox --skip-action-text --skip-spring --skip-turbolinks --webpack=react -T
```

Based on [this guide by Evil Martians](https://evilmartians.com/chronicles/graphql-on-rails-1-from-zero-to-the-first-query).

It’s strongly recommended that you disable all the unnecessary generators in the  config/application.rb:

```
config.generators do |g|
    g.test_framework  false
    g.stylesheets     false
    g.javascripts     false
    g.helper          false
    g.channel         assets: false
end
```

## Models

Item to describe any entity (book, movie, etc.) that we want to store in the library.

User to represent the application user who can manage items in the collection.

```
rails g model User first_name last_name email
rails g model Item title description:text image_url user:references
```

Add the has_many :items association to app/models/user.rb.

Add some pre-generated data to db/seeds.rb.

## GraphQL

```
bundle add graphql
rails generate graphql:install
```

Add the following lines to app/assets/config/manifest.js:

```
//= link graphiql/rails/application.css
//= link graphiql/rails/application.js
```

Create types:

```
rails g graphql:object user
rails g graphql:object item
```

## Front End


```
yarn add apollo-client apollo-cache-inmemory apollo-link-http apollo-link-error apollo-link graphql graphql-tag react-apollo
```