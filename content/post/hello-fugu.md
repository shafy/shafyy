---
title: "Hello, Fugu"
date: 2021-10-28T17:00:00+02:00
draft: false
---

Yesterday, I went live with [Fugu](https://fugu.lol). Fugu is a product analytics software that focuses on simplicity and privacy, and is open-source and self-hostable.

Here's how it looks:

![Fugu Screenshot](https://fugu.lol/images/fugu_screenshot_main.png)

### How it works

The idea is that you send your events to the Fugu API, and can then analyze your data using a set of tools in the Fugu web app. When capturing an event, you can also send along optional properties that consist of keys and values. For example, you can track a "platform" property that has different values, such as "web", "android" or "ios". Properties are completely user-defined.
Fugu then allows you to break down your data by different property values to get a better understanding of how your users use your app.

This is an early version of Fugu, and many more features and improvements are planned. For example, I will add conversion funnels so that you can see where your users drop off in your flows. I also plan to add a property value filter, that allows you to look at your data in more detail.

### Pricing

I've decided to go with one pricing tier at $9/month that includes up to 1 million events per month. Fugu is aimed at smaller companies or indie hackers that don't need complex analytics solutions but prefer something affordable and simple. Going with one price reduces some complexity and also makes every customer equally important for me. Like this, I can avoid the cluster risk of having a few large customers that make up 80% of my revenue. 


### Privacy

Fugu's focus on privacy means that I need to implement common analytics features differently, or not at all. Consider the commonly used tool of retention analysis. A retention analysis helps you to see for how long a new user was retained after they first started using your product. The problem with implementing this tool is that you need to track unique users and attribute events to them over long periods of time. This is not a good thing to do privacy-wise, because it could enable someone who has access to this data to single out specific individuals.

I'm not sure yet how and if I will be able to add retention analysis to Fugu. There might be a way to do it by grouping together enough users so tracing a set of actions back to one specific user becomes impossible.

### Tech stack

Fugu is a web app built in Ruby on Rails with a Postgres database. For the static website, I use Hugo. The Rails app is hosted with Digital Ocean, and the static site with Netlify. To display the charts I use the excellent chart.js library. For payments I use Stripe (Checkout and Customer Portal). For analytics I use Fugu (whaaat?!) for the Rails app and Plausible for the static site.

Going live with a new project is always exciting but only the first step of a long journey.

Make sure to check out [fugu.lol](https://fugu.lol) to learn more about Fugu and, if you are looking for a no bullshit and privacy-friendly analytics tool, create an account and see if it fits your needs.


