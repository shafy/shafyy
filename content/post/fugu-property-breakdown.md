---
title: "Fugu: Property Breakdown"
date: 2021-10-10T13:13:00+02:00
draft: false
---

An important part of Fugu is that you can save custom properties along with your event. Your HTTP request body might look like this:

```
{
  "api_key": "very_secret",
  "name": "Fun event",
  "properties": {
    "color": "Blue",
    "type": "Oak"
  }
}
```

With the property breakdown feature, you can break down each event's property to their values. For example, if you have events with `"Blue"`, `"Red"`, `"Green"` as values for its `"color"` property, the breakdown view will show a separate line for each property value.

Have a look at this video to see it in action (with my boring test data):

<video width="100%" controls>
  <source src="/videos/fugu_property_breakdown_demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Fugu only allows one level of nesting. The values will always be saved as strings. I think that this will suffice for most use cases, and adding more complexity with a multi-level property values breakdown feature is not something I want to get into.

If you want to see how it is implemented, head over to the [repo](https://github.com/shafy/fugu) and have a look. I welcome any comments on the code itself - just open a GitHub issue.

This was the last "big" feature I wanted to build before getting ready for Fugu's public launch. Now, the only things left to do are to add a billing system (Stripe) and pretty up the UI and UX.

If you want to give this early version a free spin, head over to the [GitHub repo](https://github.com/shafy/fugu) and follow the readme to sign up. Make sure to drop me an email with your feedback: canolcer@hey.com