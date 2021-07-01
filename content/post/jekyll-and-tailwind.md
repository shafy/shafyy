---
title: "Jekyll and Tailwind: How to speed up build time"
date: 2021-06-29T21:26:00+02:00
draft: false
---

I've been trying out Jekyll for a [new side project's](https://github.com/mapzy/mapzy) static website and of course added my favorite CSS framework, Tailwind, into the mix. However, after adding Tailwind with PostCSS I began to see very slow build times. Generating the site went from less than a second to more than 30 seconds. Waiting this long to see every change you do makes working with Jekyll impossible.

The problem arises because Jekyll regenerates all of the SCSS for every change, even if you use the `--incremental` flag and don't touch your SCSS. The Tailwind files include a lot of CSS classes, and therefore this takes forever (at least on my 2016 MacBook).

There are different ways to avoid this and build your own fancy asset pipeline, but I wanted to stick to a simple asset pipeline with PostCSS.

The idea is to take advantage of some neat config options in Jekyll and of the fact that you usually don't change your Tailwind CSS. We'll make Jekyll generate the site with Tailwind once in the beginning of our project, and after that tell Jekyll to not bother with the Tailwind CSS files.


First, add Tailwind with PostCSS to your project (you can follow [this](https://mdoliwa.com/articles/how-to-setup-jekyll-with-tailwind-css) or [this tutorial](https://stevenwestmoreland.com/2021/01/using-tailwind-css-with-jekyll.html)).


Second, in your `_config.yml` file, add the following to your `exclude` and `keep_files` settings.

```
exclude:
  # other stuff you're excluding
  - assets/css/tailwind.scss

keep_files:
  # other stuff you're keeping
  - assets/css/tailwind.css
  - assets/css/tailwind.css.map
```

We're telling Jekyll to ignore `tailwind.scss` and to not delete `tailwind.css` and `tailwind.css.map` when building the site. Why not delete the files if we ignored them in the first place? You'll see. Make sure that you only `@import` the Tailwind stuff in `tailwind.scss` and keep the rest of your CSS in other files. My `tailwind.scss` looks like this:

```
---
---

@import "tailwindcss/base";

@import "tailwindcss/components";

@import "tailwindcss/utilities";

```

Third, we add a second config file called `_config_tailwind.yml` that looks like this:

```
include:
  - assets/css/tailwind.scss
```

That's it.

The magic happens here: Whenever you want Jekyll to build Tailwind, you need to tell it to include both config files. You definitely need to do this once at the start of the project, and then everytime you change something in Tailwind. To build with both configs, run this command:

```
jekyll build --config _config.yml,_config_tailwind.yml
```

After that, you can just build or serve Jekyll normally with:
```
jekyll serve --incremental
```

The `keep_files` option is necessary, because otherwise Jekyll will delete our `taiwind.scss` file from the generated site.

Bonus: To make your live easier, add the initial build command to your `package.json` file:
```
"scripts": {
  "build-tailwind": "jekyll build --config _config.yml,_config_tailwind.yml"
}
```

Now, you can just go `yarn run build-tailwind`.

A word of caution: Once you add PostCSS to handle your asset pipeline, [Jekyll's standard way of importing SASS partials](https://jekyllrb.com/docs/assets/#sassscss) from the `_sass/` folder stops working. Instead, you need to import with the full path, like so:

```
# assets/css/main.scss

@import '/_sass/header.scss'

# this default Jekyll way will fail
@import 'header'

```