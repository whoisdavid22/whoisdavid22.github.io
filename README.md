# AgroSentinel

AgroSentinel is a project we built for the Intel InNow Technology Fest 2026, aimed at solving a pretty concrete problem: on many farms, irrigation happens out of habit, not because anyone actually checked whether the crop needs water that day. That means sometimes crops get overwatered and water gets wasted, and other times a crop goes through water stress without anyone noticing in time.

The idea behind the project is simple: build a system that watches the crop all the time, decides when to irrigate using the same logic an agronomist would use, and acts on its own, without anyone having to be paying attention all day

You can try it here: [whoisdavid22.github.io/agrosentinel](https://whoisdavid22.github.io/agrosentinel/)

## How it works, in simple terms

The system takes in field data: how much moisture is in the soil, the temperature, whether it has rained, what growth stage the crop is in, what type of soil it is, and what's being planted. That data can be entered by hand, but it can also come from an aerial photo that gets analyzed automatically, or just from sending a message on Telegram

Before asking the AI anything, we calculate how much water the crop needs that day using real agronomic formulas. We don't let the AI make up those numbers, we first run the math with real methodology, and only after that do we hand those results to Claude so it can decide what to do with that information. Claude then decides how open the irrigation valve should be, explains why it made that decision, and even says how confident it is in its answer

One part we really like is that the system doesn't always ask for the same external data. Before deciding, Claude evaluates whether it actually needs to check the rain forecast or NASA's data, and only pulls that information when it genuinely helps make a better decision. It's not a fixed process that always does the same thing the agent itself decides what information it needs

## What it does besides irrigate

Over time, the system also learns. It compares what it predicted against what actually happened on each plot of land, and adjusts its own calculation for that specific farm, within a safety limit so it never drifts too far off.

When several plots are connected to the same water source and water starts running low, each plot has its own agent that negotiates with the agents from neighboring plots, with a mediator that helps reach a fair agreement. The system even remembers who gave up water before, to take that into account the next time water needs to be shared.

We also connected a Telegram bot, so anyone can link their account and ask the system how their plot is doing, report something by just writing normally, like texting a person, and get alerts without needing to open any app.

And so we wouldn't just rely on manual tests, we built a feature that runs the same calculation day by day using real climate data from the last ninety days, to see how the system would have behaved under real conditions, not just in the examples we set up ourselves.

## What it's built with

The dashboard is built in React with TypeScript, using Vite and Tailwind for the design, Framer Motion for the animations, and Three.js for the 3D valve model. All the data flow and automation logic runs on n8n, which is what connects the dashboard to Claude, to NASA's public API, to the Telegram bot, and to Supabase, where we store each user's information under their own account, with security set up so no one can see another person's data.

## Where the science comes from

The calculations for how much water a crop needs follow the FAO-56 methodology, which is the international standard for this (Allen, Pereira, Raes, and Smith, 1998, published by the FAO). And the specific values we use for coffee, beans, tomato, sweet pepper, and corn aren't something we made up: we pulled them from a real agricultural engineering thesis from the Costa Rica Institute of Technology (Quesada Rodríguez, 2017), which studied exactly this for crops in the country's northern zone.

## Why it matters to us

This project connects directly with three Sustainable Development Goals, Zero Hunger, because it helps prevent crop loss from water shortages that go unnoticed too long; Clean Water and Sanitation, because irrigation becomes something that responds to actual need instead of a fixed schedule; and Climate Action, because it helps crops adapt better to an increasingly unpredictable climate.

## If you want to try it

You don't need sensors or a drone to try the system. Just create an account (with email or Google), move the panel controls to simulate field conditions, pick a crop, and hit analyze. You can also check out the edge cases tab to see how the system reacts when we feed it contradictory data, or try the historical validation feature to see how it would have behaved over the last few months using real climate data.

---

Built for the Intel InNow Technology Fest 2026, 6th edition.
