---
title: "Thoughts on OpenCode"
description: "The v1 harness and OpenCode Go"
pubDate: 2026-09-18
---

## Harness

OpenCode is my harness of choice at the moment, both at work and on personal devices. It's a pretty good [zero-config](https://ghostty.org/docs/config#zero-configuration-philosophy) harness. I use it a few different ways:

- Locally on...
  - My work laptop for all agentic work like coding, but also searching Webex, docs, our issue tracking system, and more.
  - My personal laptop. I do most coding on a remote server, but I've used it here for things like improving the efficiency of my system (T14 gen2 running Omarchy)
  - My desktop. One interesting thing I've done here is automating the process of ripping Blu-Rays, transcoding, and storing these on my NAS.
  - My [homelab](/blog/homelab) server. I've used this for basically all setup tasks once the OS was installed. 
- Remotely over Tailscale on...
  - My phone and other personal devices, connecting to the [web application](https://opencode.ai/docs/web/). This means I can vibe configure infra on my lunch break or on the couch at night!
  - On my desktop I've been opting for the [Desktop app](https://opencode.ai/download) (currently in beta). It offers the same functionality as the web app, but it's easier to keep track of a desktop app than a browser tab.

OpenCode is pretty good at configuring itself - it has a built-in skill `customize-opencode` for editing its own config. You can just tell it to configure an MCP or plugin, and it will probably get 90% of the way there on its own.

One thing I've ran into is OAuth issues when adding new MCPs, because the auth flow expects the terminal (on `homelab1`) to be on the same host as the browser (my desktop or laptop), which it is not. This is easy enough to fix with SSH port forwarding, but it's annoying when I have to do this. I've considered writing a custom plugin for this but haven't gotten around to it.

Using `opencode debug config` is a useful check after making changes.

Speaking of plugins, [there's a lot](https://opencode.ai/docs/ecosystem/#plugins)! They also have an [SDK](https://opencode.ai/docs/sdk/). 

I haven't used their [v2 release](https://opencode.ai/v2/docs) much, but it has some nice changes like a default password when running the web server.

## OpenCode Go

[Go](https://opencode.ai/go) is my provider of choice for my personal use. I don't want to be locked into a single model family (Claude, GPT, GLM, etc.), but I obviously don't want to pay API prices for models either! So for $10/mo you get, at minimum, $15 of [usage](https://opencode.ai/docs/go/#usage-limits) for their models included in Go. There are limits in place for 5-hour / weekly / monthly chunks.

Some models have up to $60/mo in usage because of [bulk discounts or reserved capacity](https://opencode.ai/docs/go/#why-some-models-have-lower-usage). **I definitely recommend using the models with $30 or $60 usage!** Many of these (Deepseek V4.1 Flash, Muse Spark 1.3, GLM-5.3-Flash) perform nearly as well as the lower use models, and you get to use these MUCH more than you'd otherwise get to for $10/mo.

## Closing

There's a lot of harnesses and it's a bit overwhelming trying to learn and compare new ones. I continue to use OpenCode because it's what I'm used to. I'm also playing with Pi and Hermes a bit, but they haven't stuck (yet). Go continues to offer tremendous value for my personal work, and there isn't a great alternative available elsewhere.
