---
title: "Separation of Power for programming tools and deployment infrastructure"
date: 2024-03-15T14:49:00Z
draft: false
---

In the past few years, a new trend has emerged among programming runtimes and frameworks: Trying to make money by offering deployment infrastructure, and tying some aspect of the runtime or framework to it. For example, Deno, a JavaScript runtime, offers their own cloud where you can deploy your Deno apps. They recently also launched Deno KV, a database that's well-integrated with Deno. The catch is that if you don't want to use Deno's deployment infrastructure, you need to run your own self-hosted version of their database.

Similar is the case with Astro DB, a database started by the makers of the framework Astro. Another example is Prisma, a ORM (Object Relational Mapping) library for popular databases. Free, open-source software, but if you don't use their hosted, paid service, you need to jump through quite a few hoops to get started.

Why do these services create their own database and not just use one of tried and true database programs like PostgreSQL, Redis or SQLite?

> "Prisma Raises $40M to Build the Application Data Platform"

> "I am thrilled to announce the creation of The Astro Technology Company along with $7M in seed funding to help us build a better platform for web development."

> "The Deno company has raised $21M in an investment round led by Sequoia Capital with participation from Nat Friedman, Four Rivers Ventures, Insight Partners, Long Journey Ventures, Dylan Field, Automattic, Netlify, and Shasta Ventures"

Fueled by VC money, they need to find a way to make their investors' cash back, and quickly. Inevitably, this desperate attempt to lock in programmers who use these once free tools, will lead to the downfall of these companies. Whatever promise they may hold, their path of Enshittification began the second they started sucking on that sweet VC teet. It will only get worse from here on.

Programming tools like runtimes and frameworks should be separate from deployment infrastructure, so that we can avoid conflicts of interest. It's almost like the separation of power in governments between executive, legislature and judiciary branches.