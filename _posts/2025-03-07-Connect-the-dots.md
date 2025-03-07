---
layout: post
title: "Connect the Dots #1"
date: 2025-03-07
categories: cs 
author: Remy
description: "Dots #1"
github: https://github.com/Rae699
comments: false
---

# Dots #1 — From 28K Lines of Vibes to Billions of Data Points

Two months ago, I built **Dots**.

Armed with AI (mostly Claude Sonnet 3.5), curiosity, and zero formal CS knowledge, I threw myself into code. 
After **401 hours**, **5000 AI prompts**, and **27,887 lines of code**, *Dots* became a reality:  
A fully automated, multi-exchange **signal screener** scanning crypto markets across **14 timeframes**, applying my personal strategies, and outputting real-time signals through a live dashboard.

It works.  
It runs.  
It's already powerful.  

But now... it's time to scale *Dots* beyond what vibe coding can support.  


## 📊 Proof of Work

#### 🚀 **Total Lines of Code: 27,887**

![Git Fame 27,887 LOC](git-fame-27887.png)

---

#### ⏳ **401 Hours of Coding Time in 2 months**

Tracked via **WakaTime**:  

![WakaTime Dashboard](wakatime-dashboard.png)


---

## 🧠 What Is *Dots*?

This is the project that forced me to take Computer Science seriously.

### The v1 story:
It started as a **2,500-line monolith** — a single script handling everything from fetching data to generating signals and printing results.

And yeah, it worked...  
But it was duct tape.  
Unscalable. Unreadable. Unmaintainable.

### The v2 upgrade:
I completely **refactored it into a modular architecture** — **65 separate modules** — making it possible to:
- Plug in new strategies.
- Add exchange integrations.
- Scale across assets and timeframes.
- Maintain and debug specific features without breaking the entire system.

![Dots Folder Structure](dots-src-organziation.png)

Today, *Dots* is:
- ✅ Screening all cryptocurrencies on Binance listed as perpetual.
- ✅ Running multiple custom strategies (RSI divergences, relative strength, trendlines, etc.).
- ✅ Handling multi-timeframe analysis (up to **14 per asset**).
- ✅ Outputting real-time, visual HTML screeners.
- ✅ Modularized into **65 distinct modules**.
- ✅ Fully automated, with thousands of requests running daily.

And yet… despite building it, I still don't fully understand how Dots works end to end.
That's the gap I'm here to close.


---

### 🧠 And what does AI say about *Dots*?

![What AI Says About Dots](what-ai-says-about-the-dots.png)

Apparently, I accidentally built something that looks like the work of a developer with **5–10 years of experience**.  
That's flattering. But now it's time to **earn it for real**.


---

## 🔍 Where We're Going  

Now I want *Dots* to do more:  
Screen **80,000 stocks per day**, across **14 timeframes**, refreshing **multiple times a day**.

Which means:

> **Billions of API calls. Billions of data points. Every single day.**

This isn't about just adding more power.  

This requires **rethinking everything**:  
- The architecture.  
- The data flow.  
- The algorithms.  
- Later on, the languiage choices.

And that starts with two key steps:


---

## Step 1 — Add **Tracing**

Right now, *Dots* works… but I don't know exactly why or how efficiently.  

### What I need:
- Full visibility into every request, loop, and computation.
- Detection of redundant operations, duplicate data pulls, and wasted cycles.
- Clear metrics on bottlenecks and performance killers.

We can't scale what we can't see.


---

## Step 2 — Refine and Optimize  

The core concepts are already in *Dots*:
- ✅ Async requests.
- ✅ Caching layers.
- ✅ Batching strategies.
- ✅ Retry and rate limiting.
- ✅ Parallel computations.

But these were **bolted on with AI's help**, scattered across modules, and never fully optimized or designed as a cohesive, scalable system.

Scaling to billions of data points isn't about having these tools — it's about **mastering** them:
- Choosing the right algorithms.
- Reducing complexity.
- Profiling and eliminating bottlenecks.
- Picking the right languages when necessary.
- Engineering caching and data pipelines to perfection.

This is where **Computer Science** comes in.


---

## 🚀 Why This Blog Exists  

This blog isn't about showcasing some perfect system.  
It's about showing the real work:  
The transition from **AI-assisted chaos** to **engineering mastery**.  
From duct-taped prototypes to scalable, production-grade systems.

I'm not here pretending to be a senior engineer.  
I'm here documenting the climb — the moments where I don't understand, the parts where I'm lost, and the breakthroughs that follow.

The mission now is clear:
- Build real coding skills, from syntax to system design.
- Master algorithms and architecture.
- Refactor *Dots* into something I can proudly call **Google-scale**.
- Leave behind vibe coding and take full ownership of my stack.


---

### 🚀 This is part of a bigger story.

- 👉 [Start Here]({{ site.baseurl }}{% link start-here.md %}) to see why this whole blog exists.  
- 👉 [Read my first post]({{ site.baseurl }}{% post_url 2025-03-03-my-first-post %}) to see where it all began.  
- 👉 [Check out my deep dive on SICP]({{ site.baseurl }}{% post_url 2025-03-09-SICP-1 %}) to follow my CS journey and learning path in parallel.  

*Dots* is just one chapter. 

But it's the chapter that's forcing me to level up, fast.


---

## 📌 Coming Up in *Dots #2*  

An insane level-up arc incoming:  
- Mapping the full architecture of *Dots*.  
- Adding tracing and profiling to finally measure what's happening under the hood.  
- Hunting down and eliminating inefficiencies.  
- Planning the first big refactors and optimization passes.  

This is where vibe coding ends.  
This is where real engineering begins.  

Thanks for following along.

