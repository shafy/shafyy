---
title: "In product analytics, apply the Pareto principle"
date: 2022-03-27T16:31:12Z
draft: false
---

Approaching product analytics with the [Pareto principle](https://en.wikipedia.org/wiki/Pareto_principle), also known as the 80/20 rule, will help you to make better product decisions and protect your users' privacy. Let's see how.

Understanding how your customers use your product is important. A good way to improve that understanding is to track things your users do in your app. Typically, you would track events like users signing up, viewing relevant pages, clicking buttons, users upgrading or downgrading their subscription and so on.

However, there’s a real danger of having too much data.

I’ve seen it countless times at different companies. People become addicted to collecting data. They want to track every little thing and go into panic mode when they realize there’s some action somewhere that they are not tracking.

This is not good. Too much data makes analyzing data harder. It’s becomes more difficult to discern between signal and noise. This leads to confusion and unhappiness. In the end, people stop looking at data altogether because it becomes too much of a chore.

Developing products should be an orchestra of quantitative data, qualitative user feedback, your expertise, your creativity and your goals with the product. Focus too much on any one of these factors, and you start making bad decisions.
It’s important to view data from user tracking just as one ingredient, not the whole meal. It’s easy to fall into a trap where you start optimizing for one metric. Unsurprisingly,  your data will tell you that this metric has improved, so you keep doing more of the same. This will almost always take you on the wrong path. A path where you miss the forest for the trees.

Furthermore, there's the topic of privacy. If you collect too much data, it also becomes increasingly harder for you to guarantee the privacy of your users. Especially if you track unique users. It has become common practice to track unique users, and most people just do it without weighing the pros and cons. In a [different article](https://fugu.lol/why-fugu-doesnt-track-unique-users/), I argue that tracking unique users is not worth its privacy trade-off.

Industry standard product analytics tools like Mixpanel and Amplitude track unique users per default. They also encourage you to track every single thing your users do and provide you an arsenal of analytics reports. Of course, they do - the more you track, the more money they make.

The reality is, that most people don’t need fancy reports like cohort analyses, retention reports and attribution reports. If you aren’t an experienced data analyst, you will have a hard time deriving actionable insights from these reports. Even if you know what you’re doing, the additional value from these fancy reports will be small for most products and companies.

These are some of the reasons why I work on [Fugu](https://fugu.lol). Fugu is a product analytics tool that doesn’t track unique users, and focuses on a few simple reports only, taking an efficient Pareto approach.