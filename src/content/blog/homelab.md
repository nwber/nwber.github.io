---
title: "Homelab - getting started"
description: "For fun and profit"
pubDate: 2026-08-25
---

## Why

Historically I've always wanted my personal devices to "just work". I mean, why would I want to bang my head against infrastructure all day at work just to do it after work (and not even be paid for it)?

The last couple years I've experimented with VMs on Hetzner and bare metal on OVH Cloud for side projects. They're useful and pretty affordable! However, in June Hetzner [tripled their prices](https://docs.hetzner.com/general/infrastructure-and-availability/price-adjustment/) for new instances (thanks, Sam Altman) and I don't see things getting better any time soon. Used hardware on eBay is still *relatively* cheap, and the economics can make sense if the power draw is low.

My use cases have also changed: instead of running a dumb FastAPI app on a small VM, I want to run several local services that actually provide value to me. And because it's less learning exercise and more useful, I feel more motivated to actually work on it. I'll get more into specifics in the software section.

Some of the specific use cases are:

- Checking on my cats when I'm out of the house or on vacation - we don't have central air and I'm writing this as it's >95F in the Boston area. It would be nice to monitor the temperature in the rooms with AC and maybe even a live video feed.
- Movies! We've been getting into physical media lately and Blu-rays are only $4/each at Saver's. Backing these up and being able to stream them to any device is very useful.
- Education! I'm more inclined to do all of this when it's not theoretical, so trying out new tech doesn't feel like work at all!

## Hardware

Compute:

- I currently only have one "server" (will refer to this going forward as `homelab1`): an HP Elitedesk G4 800 with an Intel i7-8700, 16GB DDR4, and a 256GB SSD. I've also added an 750GB Intel Optane P4800X (with a M.2 to U.2 adapter), a NICGIGA 2.5Gb NIC, and a TP-Link USB Bluetooth adapter.
- This runs the majority of the services.
- `<include picture of homelab1>`

Storage:

- I've had a Synology DS220j 2-bay NAS for a few years, with 2x WD Gold 4TB drives in RAID 1. This is where anything large/important is stored.

Home Assistant:

- RPi4 2GB running [HA OS](https://www.home-assistant.io/installation/raspberrypi). I could run this as a container on `homelab1`, but the add-on store is only available for HA OS. I have several RPi4s laying around anyway.

## Software

`homelab1`

- Ubuntu
  - It's my distro of choice, I don't care enough to run anything more exotic
  - I would tell the Arch bros to fight me but they don't go outside
- Docker
  - It's my container runtime of choice, I don't care enough to run anything more exotic
- Tailscale
  - Lets me connect to any of my services from any of my devices. It's one of those "it just works" services that I now take for granted.
- OpenCode
  - Runs as a systemd process, so it's always in the background
- Grafana, Prometheus, Loki
  - Self explanatory
- Prometheus node exporter
  - So I can monitor the server's metrics
- Jellyfin
  - For watching Blu-rays (stored on the NAS). When the apocalypse comes, he who owns Interstellar on Blu-ray  will be king
  - I also had an agent write a script for my Windows desktop that polls for inserted disks, rips it to my NAS, transcodes it with Handbrake, and puts it in a directory that Jellyfin has access to
  - I opted for a server with an Intel CPU for the iGPU transcoding
- Dockhand
  - Web GUI for managing the various containers
  - It's free for home use! Neat
- UptimeKuma
  - Uptime monitoring service, mostly for fun but also a good external monitoring source for work stuff
  - I use [Resend](https://resend.com/) for email notifications - they even have a Cloudflare integration so they created the DNS records for me!
- Plenty more to come!

Aranet4 Home

- Monitors CO2, temperature, humidity, and atmospheric pressure
- Only accessible over Bluetooth, but it's available in HomeAssistant

First Raspberry Pi 4

- Home Assistant
  - Opted to not run as a container on `homelab1` because I want to use their apps and have it update automatically
  - I can see data from the Aranet4 Home, some Tapo smart plugs, and my Litter Robot

Second Raspberry Pi 4

- Sensors
  - For fun we can measure radiation! That's TBD...

## Next steps

In no particular order or timeline, I plan on the following:

- "Production-ize" / use best practices. Things like backups, SSL for web services, giving the agent it's own user on `homelab1`, etc.
- Improve `AGENTS.md`, add skills and MCPs to enhance capabilities, install agent-vault, make a private Discord bot for OpenCode, and more! I have lots I want to do to my agent dev environment
- Setup some kind of camera system so I can check on my cats when I'm on vacation
- Upgrade NAS and/or combine with `homelab1` (whenever hardware prices to become reasonable again)
