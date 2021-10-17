---
title: "Fugu is now prettier"
date: 2021-10-17T19:22:00+02:00
draft: false
---

For the past few months I've been working on Fugu, a simple and open-source product analytics software. I'm happy to announce that I've finished all work and am almost ready for the public launch. Need to whip up a minimal landing page before, though.

Here's a preview of two small features that I've worked on this weekend. First, I've added a dedicated page to view the project settings. There you can find the API keys that you need when calling the Fugu API and delete the project:

<video width="100%" controls>
  <source src="/videos/fugu_project_settings_demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

Second, when you break down by event property values, Fugu now sorts by descending total count and only displays the first five data sets, hiding the others. Before adding this feature, the chart was too crowded and not useful. You can simply enable datasets by clicking on them in the legend. It looks like this:

<video width="100%" controls>
  <source src="/videos/fugu_property_value_sorting_demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

If you're a keen follower of my process (haha!), you might have also noticed that I've added a header, a footer and improved some of the layout and colors.

Public launch is coming before the end of October! If you want to try an early version already now, head over to [Fugu](https://app.fugu.lol) and sign up for free. Note that the changes shown here are not live yet.