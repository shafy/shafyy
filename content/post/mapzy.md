---
title: "Mapzy, an open-source and simple store locator"
date: 2021-12-05T13:25:33Z
draft: false
---

My friend [Sag](https://twitter.com/SagGpt) and I have been working on Mapzy since April 2021, and finally made enough progress to publicly launch it.

Mapzy is a store locator and allows you to easily add locations along with a description and opening times to a map, and then embed that map in your own website.

We came up with the idea when I was still making and selling plant-based cheese. We had a couple of restaurants and grocery stores that sold our cheese, and I was looking for an affordable and simple store locator to display the locations on our website.
It turned out that most store locators are either expensive and overloaded with features or look outdated.

That's how Mapzy was born. We focus on a simple set of features (more to come!) and offer a solid experience at a fair price. Furthermore, we try to be as privacy-friendly as possible. We don't track any PII, but we still have to use Mapbox which unfortunately tracks some PII (not too bad, much better than Google Maps).

Here's a video showing the admin dashboard and how you add a location:

<video width="100%" controls>
  <source src="/videos/mapzy_demo_small.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Mapzy is [open-source](https://github.com/mapzy/mapzy) and can be self-hosted for free. Our hosted pricing starts at $9/month, which includes adding up to 20 locations to your map.

Like most of my projects, Mapzy is a Ruby on Rails application. We also have some Stimulus and Turbo in there. Futhermore, we use the ever-aweseome Tailwind library.

Our focus now will be on developing more features and getting the word about Mapzy out.

Learn more on [mapzy.io](https://mapzy.io).