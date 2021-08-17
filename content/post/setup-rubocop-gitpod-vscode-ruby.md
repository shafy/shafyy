---
title: "Setting up Rubocop correctly with Gitpod and VSCode Ruby"
date: 2021-08-17T10:05:00+02:00
draft: false
---

I've recently come across [Gitpod](https://gitpod.io/). Gitpod provides cloud-based development environments. They're similar to [GitHub Codespaces](https://github.com/features/codespaces), but in my opinion offer a better experience. Setting up an environment is simpler and they are all about ephemerality. The idea is that each environment just lives for the duration of the task you're working on, and then you throw it away. Like Codespaces, Gitpod uses the Visual Studio Code editor, which you can access with your browser.

I'm slowly adding Gitpod to all of my projects, because the development experience is much better than doing it on my local machine.

For [one of my Rails projects](https://github.com/shafy/fugu/), I had some issues getting the Rubocop linter to work. Here's a short set up guide to so that others can avoid the problem I had.

To configure your environment to work with Gitpod, you need to add a file called `.gitpod.yml` to the root of your project. In my case it looks like this:

```
image:
  file: .gitpod.Dockerfile

ports:
  # Rails server
  - port: 3000
    onOpen: ignore
  # PostgreSQL server
  - port: 5432
    onOpen: ignore

tasks:
  - init: >
      bundle install &&
      rails db:setup
github:
  prebuilds:
    branches: false
    pullRequests: true

vscode:
  extensions:
    - rebornix.ruby
    - wingrunr21.vscode-ruby
```

You can see that it contains simple instructions that Gitpod uses to set up your cloud-based development environment. Importantly, it needs to know which Docker image it will build from. While you can specify a pre-built image, in this example, I reference another file in my project called `.gitpod.Dockerfile` that looks like this:

```
FROM gitpod/workspace-postgres
USER gitpod

# Install the Ruby version specified in '.ruby-version'
COPY --chown=gitpod:gitpod .ruby-version /tmp
RUN echo "rvm_gems_path=/home/gitpod/.rvm" > ~/.rvmrc
RUN bash -lc "rvm reinstall ruby-$(cat /tmp/.ruby-version) \
              && rvm use ruby-$(cat /tmp/.ruby-version) --default \
              && gem install rails \
                 rubocop rubocop-performance rubocop-rails rubocop-rspec"
RUN echo "rvm_gems_path=/workspace/.rvm" > ~/.rvmrc
```

This is a default Gitpod Docker image that works well with Rails and Postgres. Gitpod first runs the commands in the Dockerfile, and then the commands in the `tasks:` key in `.gitpod.yml`. And here is the tricky part: If you only install Rubocop with the `bundle install` command after the Docker image has been set up, [VSCode's Ruby extension](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby) (which we use for linting) won't have access to the command. Therefore, as you can see in the above Dockerfile, you need to install `rubocop` in the same path as you install Ruby.

That's it! If you haven't tried Gitpod or Github Codespaces, I really recommend giving it a spin. For me, this is the next level of abstraction in programming that will increase developer productivity by a significant factor.