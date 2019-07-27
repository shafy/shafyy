---
title: "VPN on Oculus Go and Quest"
date: 2019-07-27T13:02:00+03:00
draft: false
---

This is pretty straight-forward. The basic idea is that you get your VPN provider's Android app and install it on your Oculus Go or Quest. Of course, this means that your VPN service needs to offer an Android app in the first place. BEWARE, I only tested with [NordVPN](https://nordvpn.com/) so far.

Let's get started.

Some quick background: The Oculus Go and Quest run Android and allow accessing your device with Android Debug Bridge (adb, a command-line tool). This means that you can install any Android app on your Go or Quest, as long as you have the source file (ending with .apk). Although not all apps can be launched on your VR headset, most of them should be good to go.

**First**, download your VPN Android app.

**Second**, make sure that you have set up your Go or Quest so that you can sideload apps into it (sideloading means installing apps directly from your computer and not over the official Oculus store). If you don't know how to do that, ask [DuckDuckGo](https://duckduckgo.com/) or, even easier, use [SideQuest](https://sidequestvr.com/).

**Third**, launch your VPN app on your VR headset. It might show up under "Unknown Sources" and/or in your Oculus TV app. In my case, it only shows up in the Oculus TV app.

**Fourth**, log in and connect to the server of your choice.

**Voilà**. Open your favorite browser or app on your headset and see if it works.

Let me know which VPN providers worked and didn't work in your case, so I can add it to this post. Discussion, questions and comments on [this tweet](https://twitter.com/canolcer/status/1155080790977515520).
