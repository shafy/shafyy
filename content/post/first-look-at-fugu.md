---
title: "Fugu: First look"
date: 2021-09-22T18:13:00+02:00
draft: false
---

A couple of months ago I started to work on a small side project called [Fugu](https://github.com/shafy/fugu). I came up with the idea because I couldn't find a privacy-friendly, self-hostable product analytics software that's priced reasonably.

[PostHog](https://posthog.com/) comes the closest. I was an early PostHog user, but they started adding too many features that I didn't care about and the whole thing got too cluttered and complicated. I want something simple.

Fugu is still in development, and I plan to launch the first public version in the coming weeks. The self-hosted version will be free forever, and I'll offer a managed version for a fair price for folks who don't care about self-hosting. Luckily, I've got some early users that are trying it out for free so I can better understand what I need to build.

How it works is pretty straight-forward. Every time you want to track an event, you call the Fugu API and tell it what the event is called and what (optional) properties it has. The HTTP POST request could look like this:

```
{
  "name": "Signed up",
  "api_key": "747482a6a53424daf3b8c85080811154",
  "properties": "{\"favorite_animal\": \"Banana\",\"type\": \"Early user\"}"
}
```

And then, you can log in to your account and look at the data. The current version is very basic and just allows to select an event and change the time aggregation (daily, weekly, monthly, yearly). Here's how it looks:

<video width="100%" controls>
  <source src="/videos/fugu_demo_1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Next, I'm working on a feature that lets your break down and filter you events by properties, as well as a date picker so that you can display custom date ranges. Of course, I'll also improve the styling and UX before launching publicly.

If you're interested in trying out Fugu already in this early state (for free), have a look at the readme on the [GitHub repo](https://github.com/shafy/fugu) to get started or drop me an email at canolcer@hey.com.

