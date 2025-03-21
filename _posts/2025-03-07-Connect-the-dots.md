---
layout: post
title: "Connect the Dots #1"
date: 2025-03-07
categories: project 
author: Remy
description: "Dots #1"
github: https://github.com/Rae699
comments: false
---

# Dots #1 — From 28K Lines of Vibes to Billions of Data Points

Two months ago, I built **Dots**.

Armed with AI (mostly Claude Sonnet 3.5), curiosity, and zero formal CS knowledge, I threw myself into code. 
After **401 hours**, **~6750 AI prompts**, and **27,887 lines of code**, *Dots* became a reality:  
A fully automated, multi-exchange **signal screener** scanning crypto markets across **14 timeframes**, applying my personal strategies, and outputting real-time signals through a live dashboard.

It works.  
It runs.  
It's already powerful.  

But now... it's time to scale *Dots* beyond what vibe coding can support.  


## 📊 Proof of Work

#### 📷 **How It Looks Like (1 of 5 screeners)**
![RSI Divergence Screener]({{ site.baseurl }}/assets/rsi_div_screener.png)


#### 🚀 **Total Lines of Code: 27,887**

![Git Fame 27,887 LOC]({{ site.baseurl }}/assets/git-fame-27887.png)

---

#### ⏳ **401 Hours of Coding Time in 2 months**

Tracked via **WakaTime**:  

![WakaTime Dashboard]({{ site.baseurl }}/assets/wakatime-dashboard.png)

---

#### 💡 **Total AI Prompts: ~6,891**

```python
# Calculating total prompts from Stripe billing
# Breaking down by month (March 2025 - January 2025)

# March 2025
march_base = 2000    # Base quota
march_extra = 505    # Extra fast premium requests
march_regular = 50   # Regular requests
march_total = march_base + march_extra + march_regular  # 2,555

# February 2025
feb_base = 1500      # Base quota
feb_extra = 556      # Extra fast premium (45 + 511)
feb_regular = 120    # Regular requests (46 + 74)
feb_total = feb_base + feb_extra + feb_regular  # 2,176

# January 2025
jan_base = 1500      # Base quota
jan_extra = 564      # Extra fast premium (288 + 276)
jan_regular = 96     # Regular requests (1 + 72 + 23)
jan_total = jan_base + jan_extra + jan_regular  # 2,160

# Total prompts across all months
total_prompts = march_total + feb_total + jan_total  # 6,891
```

![Stripe Billing for Prompt Computation]({{ site.baseurl }}/assets/stripe_billing_for_prompt_computation.jpeg)

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

![Dots Folder Structure]({{ site.baseurl }}/assets/dots-src-organization.png)

Today, *Dots* is:
- ✅ Screening all cryptocurrencies on Binance listed as perpetual.
- ✅ Running multiple custom strategies (RSI divergences, relative strength, long term/mid term pullback entries, etc.).
- ✅ Handling multi-timeframe analysis (up to **14 per asset**).
- ✅ Outputting real-time, visual HTML screeners.
- ✅ Modularized into **65 distinct modules**.
- ✅ Fully automated, with thousands of requests running daily.

And yet… despite building it, I still don't fully understand how Dots works end to end.
That's the gap I'm here to close.


---

### 🧠 And what does AI say about *Dots*?

![What AI Says About Dots]({{ site.baseurl }}/assets/what-ai-says-about-the-dots.png)

Apparently, I accidentally built something that looks like the work of a developer with **5–10 years of experience**.  
That's flattering. 

But now it's time to **earn it for real**.


---

## 🔍 Where We're Going  

Now I want *Dots* to do more:  
Screen **80,000 stocks per day**, across **14 timeframes**, refreshing **multiple times a day**.

Which means:

> **Billions of API calls. Billions of data points. Every single day.**

This isn't about just adding more power.  

This requires **rethinking everything**:  
- The architecture: implement diagram (boxes, arrows, flow of data)
- The data flow.  
- The algorithms.  
- Later on, the language choices.

And that starts with two key steps:

## Step 1 — Add **Tracing**

Right now, *Dots* works… but I don't know exactly why or how efficiently.  

### What I need:
- Full visibility into every request, loop, and computation.
- Detection of redundant operations, duplicate data pulls, and wasted cycles.
- Clear metrics on bottlenecks and performance killers.

We can't scale what we can't see.


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

I'm not here pretending to be a senior engineer.  I am  still a noob.
I'm here documenting the climb — the moments where I don't understand, the parts where I'm lost, and the breakthroughs that follow.

The mission now is clear:
- Build real coding skills, from syntax to system design.
- Master algorithms and architecture.
- Refactor *Dots* into something I can proudly call **Google-scale**.
- Leave behind vibe coding and take full ownership of my stack.


---

### 🚀 This is part of a bigger story.

- 👉 [Start Here]({{ site.baseurl }}{% link start-here.md %}) to see why this whole blog exists.  
- 👉 [Read my first post]({{ site.baseurl }}{% post_url 2025-03-03-The-Journey %}) to see where it all began.  
- 👉 [Check out my deep dive on SICP]({{ site.baseurl }}{% post_url 2025-03-07-SICP-Key_Takeaways %}) to follow my CS journey and learning path in parallel.  

*Dots* is just one chapter. 

But it's the chapter that's forcing me to level up, fast.


---

## 📌 Coming Up in *Dots #2*  

An insane level-up arc incoming: 
	•	Architecting for scale → Full system diagrams & deep dives into design trade-offs.
	•	Making it bulletproof → Unit tests, end-to-end validation, and failure handling.
	•	Peering under the hood → Tracing, profiling, and benchmarking real performance.
	•	Decision-making on bottlenecks → Exposing inefficiencies and optimizing execution paths while discussing trade-offs.
	•	Full-stack with auth
	•	Polishing: Documentation, ensuring everything including the smallest details are all working smooth.

This is where vibe coding ends.  
This is where real engineering begins.  

Thanks for following along.

