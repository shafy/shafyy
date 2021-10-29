---
title: "Rails: Prevent users from logging out after each deployment"
date: 2021-10-29T15:55:00+02:00
draft: false
---

Here's a quick one, and it may be obvious to some of you but I didn't know about it. I noticed that my Rails app ([Fugu](https://fugu.lol)) kept logging out all users after every deployment.

First, I thought it's an issue with Devise, but it turns out that it's related to a variabled called `secret_key_base` that Rails uses to sign and encrypt cookies (among other things).

For production, there are multiple places to define `secret_key_base`. A glance at the [Rails soure code](https://github.com/rails/rails/blob/9f980664fc1bc1fb9845e17d2c5a9ab710156303/railties/lib/rails/application.rb#L411-L419) shows that Rails looks for it in `ENV["SECRET_KEY_BASE"]`, `credentials.secret_key_base`, or `secrets.secret_key_base`.

In my case, I hadn't set up any credentials or secrets, nor was I providing an environment variable.

Digital Ocean (and, [as it looks, Heroku](https://blog.heroku.com/container_ready_rails_5#secret_key_base)) automatically sets the `SECRET_KEY_BASE` environment variable for you, and it changes with every deployment. And this was the problem. After each deployment, my Rails app couldn't decrypt the existing session cookies anymore beause `secret_key_base` had a different value, and my users needed to log in again.

To solve the problem, just provide a `SECRET_KEY_BASE` environment variable in your production server. The simplest way to generate it is to run `rake secret` in your terminal (make sure you're in a Rails project folder).