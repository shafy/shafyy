---
title: "Thoughts on Bluesky"
date: 2024-11-18T18:25:00+03:00
draft: false
---

Let's talk about Bluesky, the decentralized microblogging application that's currently eating Twitter and Mastodon's lunch. Or so some say.

In this post, I will explain what Bluesky is, what the problems with it are, and what we (or the team at Bluesky) can do to solve them.

## What is Bluesky?

Bluesky is a microblogging (fancy word for something like Twitter) service on the internet. It is owned by the company Bluesky Social, PBC. For the purpose of this post, it is important to distinguish between the service Bluesky and the company Bluesky Social, PBC, and I will therefore be specific about it.

What is special about Bluesky, except that it is not yet owned by Musk, is that it is decentralized and federated. Decentralized and federated means, that by following a certain set of rules (called a protocol), other apps can also interact with Bluesky. Just like you can send an email from a Gmail account to a Yahoo account. The big advantage of this for users is that they can easily switch from one service to another without losing their followers and followees.

In theory, this sounds great for users. If Bluesky fucks up, you just go to Redsky or whatever. Just like you can switch from AT&T to Verizon and still keep drunk texting your ex.

There are other social media that use open protocols. A popular one is Mastodon. Mastodon has been around for longer than Bluesky (since 2016, Bluesky since 2021), but has fewer users (8 million). Mastodon also uses a decentralized and federated protocol called ActivityPub. The protocol used by Bluesky is called AT Protocol, or ATProto, for short.

Why didn't Bluesky just use the same protocol as Mastodon? Great question, but it looks like the team at Bluesky "had their reasons", and this would be a whole other can of worms I don't want to open in this post.

Crucially, ActivityPub in its earliest form has been around for 12 years, much longer than ATProto, which started with Bluesky 3 years ago. ActivityPub is developed by the internet standards body World Wide Web Consortium (W3C), which has hundreds of member organizations and develops important standards like HTML and CSS. ATProto is developed by only one company, Bluesky Social, PBC.

## What are the problems with Bluesky?

The main problem with Bluesky is that it's not a decentralized and federated service, and it will never be one. Wait, didn't I just say a moment ago that it was decentralized and federated? Am I full of shit? I could be, but I'm not. And here's why:

The company behind Bluesky is a for-profit company with a big bag of venture capital money ($23 million). They are the only ones developing the protocol that Bluesky uses and is supposed to allow for a decentralized network. They pinky-swear that they will stay open, but their incentive to make a lot of profit is not aligned with their incentive to create an open network. For the latter, there is no incentive, except that the current management team thinks it's The Right Thing to do. Therefore, they will prioritize growing their own user base. This is already evident today, where all 19 million users of the AT Protocol are on a service run by the company behind Bluesky. There is no decentralization, and the situation for sure won't get better as the pressure for the return on investment grows on Bluesky.


Let's dive into the details to better understand the problems with Bluesky.

### Where are all the servers?

My strongest argument that Bluesky is not decentralized is also the simplest: Just look at the facts. They boast 19 million users (and growing at a rate of 10 users per second as I'm writing this), and all of them are on the server (called Relay in ATProto speak) run by Bluesky. Contrast that to Mastodon, which consists of almost 10,000 different servers, run by independent people or organizations.

Now, I need to get a bit technical here to better explain the situation. Bluesky does not have servers in the same sense that Mastodon or email have servers. Rather, Bluesky has 3 main components, that, combined, are something like a server at Mastodon. The components are: Personal Data Server (PDS), Relay and AppView. Very simplified, your posts are saved on a PDS, a Relay pulls in your posts, and the AppView reads the post from a Relay. A PDS can tell a Relay "Hey, please pull in my posts". Finally, an AppView can decide from which Relays to pull in posts.

Right now, Bluesky Social, PBC, the company behind Bluesky, runs all three components. There are a few folks running their own PDS and telling the Relay run by Bluesky Social, PBC to pull in their posts, so that they can also interact with all the other people who are using the main Bluesky PDS (that's the one you sign up to if you create a new account in the app).

Here comes the issue: Relays cannot talk to Relays. If Bluesky Social, PBC decided to show ads (or do something else you don't like), it would be very hard for you to switch to a different Relay and still be able to interact with all the other folks who stayed at the Bluesky Social, PBC Relay. Of course, if enough people decided to all switch to a new Relay (and a new AppView) at the same time, this could work. But this would be akin to everybody switching to a completly new service.

Compare this to Mastodon, where you can easily switch to a new server and most your follower won't even notice and business as usual carries on.

That's the reason why, if you look at today's landscape, there are no alternative Relays to the main one run by Bluesky Social, PBC.

Bluesky Social, PBC could change ATProto so that it's possible for users to switch to a new Relay and still be able to interact with everybody else on other Relays. Doing this will, of course, complicate the Bluesky service, a point that is often made when comparing Bluesky to Mastodon. That it's much easier, because you don't need to care about servers, and you can search and find posts and users easily. Well yes, but that's because it's fucking centralized. There are certain inalienable trade-offs that come with decentralization, and Bluesky Social, PBC has decided to not make them but still pose as an open protocol. They cannot have their cake, and it it, too.

Now, let's see why Bluesky Social, PBC does not have an incentive to create a truly open protocol.

### ATProto is decentralized, but it's proprietary

Another issue I take with ATProto is that it's developed only by one organization, Bluesky Social, PBC. They can solely decide on the future of ATProto. They could stop developing it openly tomorrow. They can decide on what changes to make or not make. Compare that to ActivityPub, the protocol used by Mastodon and others. ActivityPub in its earliest form has been around for 12 years, long before Mastodon started, and will be around long after Mastodon is gone. It is developed by W3C, the main body that develops standards for the internet, such as HTML, CSS and XML. The W3C has hundreds of members.

As I said before, Bluesky Social, PBC, currently has no incentive other than "being nice" to keep developing ATProto for the benefit of the public, and not primarily for their own benefit. I think this clearly shows the decisions they have taken so far.


### Bluesky Social, PBC is a for-profit company owned by venture capital

The thing with for-profit companies is, well, they need to make a profit. Not only that, but their main purpose is to maximize profit and the "value" they generate for their shareholders. The current management of Bluesky Social, PBC might be motivated ideologically and think that investing money and time into making ATProto truly open is The Right Thing to do, but they will cave in the long-term. There's an excellent [article by Cory Doctorow](https://pluralistic.net/2024/11/02/ulysses-pact/) that goes into the why's: But in a nutshell, if your incentive as a company is to maximize profit and grow huge to make your VCs their money back, you will start rationalizing away your ideological points one by one over time.

For Bluesky, this means that the harder it is for their users to switch from the servers and apps, the more money they can make. Therefore, they will keep making switching harder. As we have seen, that's already baked into ATProto as of today. This trend will only go in one direction.

## How can we solve the problems with Bluesky?

So, what can we do to solve these issues? You or I can't do much, but the team at Bluesky Social, PBC could do a few things to ensure the long-term viability of ATProto as a truly open, decentralized and federated protocol.

The most important thing: They can turn over ATProto to an existing standards group such as W3C to ensure that it can be developed independently of their for-profit company and by consensus of many, not driven by a single organization.

Furthermore, they can try to merge ATProto with ActivityPub somehow, so that we don't have two competing, incompatible protocols that allegedly pursue the same goal.

Finally, they can become a non-profit company. Although this one is very hard to do after taking in all the investment money. And, as we have seen in the case of OpenAI, there are no guarantees that they could switch the flip and turn back into a for-profit company for later. But it would be a strong sign and commitment to the future open social media.


## Still better than ExTwitter

To be clear: I want Bluesky to succeed and become a truly open network. However, I don't see it happening the way things are going now. Should use stop using Bluesky? No, it's still better than using ExTwitter – at least they are currently not owned by a fascist man-baby, and the Trust and Safety team at Bluesky seems to be doing a good job. But be aware that you won't be able to just pack up your followers and switch to competing service on ATProto if one day Bluesky starts going south. That's something that you can do at Mastodon. And sure, Mastodon is far from perfect and comes with its own set of problems, but at least it is decentralized.

I will keep using Bluesky and Mastodon for now. I find interesting content on both. But I will not live under the illusion that Bluesky is the same as Mastodon when it comes to decentralization and openness.



