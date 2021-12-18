---
title: "Active Record Callbacks shouldn't modify other records"
date: 2021-12-18T09:46:28Z
draft: false
---

In Ruby on Rails, After Record Callbacks allow you to hook into the lifecycle of Active Record objects. Commonly used callbacks are `after_create` or `before_validation`. In this post, I want to highlight a bad practice that is sometimes used in callbacks.

Let's say we have a `User` model that has an associated `Account`. The idea is that every user also has an account, which we use to specifiy more details like billing information.

Now, since every time we create a new `User`, we also want to create a new `Account`, we might be tempted to do something like this in our `User` model:

```ruby
class User < ApplicationRecord
  has_one :account
  after_create :create_account

  def create_account
    Account.create(user: self)
  end
end
```

This is almost never a good idea. Creating or updating one model should never touch another model.

The main reason is that it tangles up concerns (remember: we like separation of concerns) and is not very explicit. A colleague working with you on this codebase might not expect that this side effect will happen. After all, in other places in your code where you create your user, you only do `User.create` and it magically also creates an `Account` for this user.

Another reason is that, while most of the time you want to create an associated `Account`, maybe there will be times where you don't.

A further reason is testing. If you use factories to set up your test data, creating a `User` factory instance will not automatically create an `Account` factory instance, but it will create an `Account` record in the test database. Things will get messy from there.

Instead of using a callback, I recommend just creating the Account separately or wrapping these two commands into a method that lives in the `User` model, like this:

```ruby
class User < ApplicationRecord
  has_one :account
  
  def self.create_with_account(attributes)
    user = User.create(attributes)
    Account.create(user: user)
  end
end
```