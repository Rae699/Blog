---
layout: post
title: "Vibe Coding and the Ceiling No One's Talking About"
date: 2025-03-30
categories: cs 
author: Remy
description: "Opinion"
github: https://github.com/Rae699
comments: false
---

# Vibe Coding and the Ceiling No One's Talking About

![graph-diminishing-returns]({{ site.baseurl }}/assets/graph-diminishing-returns.gif)

## Chamath's Take Was Bold. I Had to Answer.

On March 27, 2025, Chamath Palihapitiya posted a viral tweet:

> "Unfortunate but accurate. The engineer's role will be supervisory, at best, within 18 months. Building tools for them will be roadkill for the model makers product roadmap." [source](https://x.com/chamath/status/1905270472947704141)

As someone who has spent thousands of hours in Cursor and Replit, building AI-generated systems, this didn't sit right with me. I had to speak up. I posted the following reply, based on my lived experience as a "maxi Cursor and Replit user."

> As a maxi Cursor and Replit user, I can share my opinion:
>
> - 6500 prompts to generate ~80 modules (Python, JS)
> - ~28,000 lines of vibe coding
>
> And I respectfully think you got this all wrong.
>
> AI is good at syntax, but... that's it. Definitely, don't spend much time on syntax issues as AI's capacity to resolve them is ~100%.
>
> BUT (and it is a massive but):
>
> AI sucks at:
>
> - Writing complex, efficient, readable, and maintainable code across a whole codebase.
> - Thinking in systems.
> - Choosing wisely (assessing the tradeoffs of X and Y).
>
> => You literally have no idea about the amount of redundancy AI coding creates... like, it is just insane.

That tweet got 12.8K views. But views don't mean agreement. Some loved it. Some pushed back. And a lot of folks misunderstood what I was trying to say. 
So here's a longer-form breakdown.

I'm not anti-vibe-coding. I'm pro-context. I'm pro-engineering. 

And I'm deeply concerned that we're speeding into a wall of **diminishing returns**, but everyone is still clapping.


---

## Are You Wondering WTF Vibe Coding Is?

If you're new here, vibe coding is the idea that with tools like Cursor, GPT-4, Claude 3.5/3.7, Replit, and others, you can build full applications by describing what you want in plain english.

It goes something like this:

> "Hey AI, build me a calendar app that integrates with Google Calendar, pulls in local events, and makes suggestions based on the weather."

And boom. 20 minutes later, you're looking at a working PWA with event cards, API calls, and a responsive UI. You didn't write a line of code manually.

I've done this. And it *does* work.

But here's the uncomfortable truth:

Vibe coding works *beautifully*... **until it doesn't.**

That moment comes fast. You go from "AI is my copilot!" to "WTF is this soup of duplicated helper functions and malformed async calls?"

You spend a lot of time unraveling what AI wrote, like a lot...


---

## The Double-Edged Sword of Diminishing Returns

![Law_of_diminishing_returns_revised]({{ site.baseurl }}/assets/Law_of_diminishing_returns_revised.avif)

### 1. The Vibe-coder Development Paradox

The first few days of vibe coding are euphoric. Every prompt gives you clean, functional code. You're in the **Productive Phase**.

Then the cracks appear:

- You ask for a refactor, and it breaks 5 dependencies.
- You prompt a new feature, and it re-implements existing logic with subtle inconsistencies.
- You try to scale your system, and realize nothing was built with coherence.

Welcome to the **Diminishing Returns** phase.

And if you keep pushing without resetting?

You hit **Negative Returns**: more code = more problems. More prompts = more bugs. 
Your productivity goes *down*.

> I've personally lived through all three stages.
>  
> 6500 prompts. 28,000 lines. I'm not guessing here.


### 2. My Real Usage: A Case Study in Pain

> You want to know what 28,000 lines of vibe code feels like?

- Redundant functions everywhere.
- Prompt drift (where AI forgets what it built before).
- Every feature request might break three other things that require constant testing/debugging.

It's not that AI is bad.
It's that we're pretending it's more than it is.

You still need software engineers. Not just prompt writers.


### 3. The LLM Capability Plateau

![LLMs-coding_capabilities]({{ site.baseurl }}/assets/LLMs-coding_capabilities.jpeg)

People look at these GPT Elo charts and think: "The machines are here. They're better than us." While the AI industry touts exponential improvements in LLM capabilities, the reality for end users tells a different story:

- **The Marketing vs Reality Gap**: Despite claims of exponential growth, the incremental improvements in practical applications remain modest
- **The Plateau Effect**: We're seeing diminishing returns in real-world performance improvements, my opinion comes from hands-on experience
- **The Cost-Performance Trade-off**: Each marginal improvement requires exponentially more computational resources and training data

> My main take is simple: **LLMs simulate IQ. They don't possess it.**

Let me explain:

- LLMs are **massive pattern matchers** trained on textual data.
- Their outputs are statistical predictions — not reasoned conclusions.
- They don't *know* what they're doing.
- They don't *understand* goals, tradeoffs, consequences.

A model with 3000 Elo on Codeforces is just *very good* at predicting the next token in a programming problem. That doesn't mean it generalizes.

IQ, in the human sense, is about *transferable*, *goal-driven*, *meta-aware* problem solving.

LLMs don't have that.

So yes, they can simulate expertise. But when you push beyond narrow patterns, they break.

And if you're building something new — and not just cloning CRUD apps — you *will* push beyond those patterns.

The question isn't whether we've reached the plateau (i think we are currently plateau'ing), it's whether we're willing to acknowledge it. 

The signs are there:

- Stagnating practical applications despite larger models
- Increasing costs for marginal improvements
- The law of diminishing returns applying to both development and capabilities

This isn't pessimism, it's realism. Understanding these limitations is crucial for setting realistic expectations and making informed decisions about AI adoption and development strategies. 


## Claude 3.7 Didn't Jump. And That Matters.

Everyone expected Claude 3.5 to 3.7 to be a leap. It wasn't. It felt like a plateau.

You can feel it when you prompt. The hallucinations are subtler. The redundancy is less obvious. But it's still there. The brittleness hasn't vanished.

The illusion of exponential gain is being shattered by the reality of marginal improvements.

> Scaling a car won't get you from Paris to London. At some point, you need a plane.

LLMs are cars. Faster and faster ones. But not planes.

They can't take you from Paris to London as they don't know how to cross the sea.


---

## So Where Do We Go From Here?

Here's the big reveal:

> **AI tools are like calculators. You still need the engineer.**

I am not an engineer but the end-user of LLMs and i deeply think that engineers are absolutely not being replaced. 
They are being challenged.

Challenged to:
- Think in systems
- Understand architecture
- Be selective in what they offload
- Know where automation ends and craft begins

If you're not an engineer, but you want to build big with AI?

You need to **learn CS**.
You need to **grind systems thinking**.
You need to **get past vibes and into architecture**.

Exactly what i am doing after hitting the vibe-coder ceiling

![vibe-coding-ceiling]({{ site.baseurl }}/assets/vibe-coding-ceiling.png)


---

## Final Thoughts: It's Not Hate. It's Love + Honesty

I love vibe coding. I use it daily. I've built amazing stuff with it.

But I've also hit its limits. Hard.

So here's what I believe:

- Vibe coding works best at the **beginning**.
- Engineers are more important than ever.
- LLMs are expanding access, not replacing expertise.
- You must treat AI as **a collaborator**, not a contractor.

We're not in the "AI is eating your job" phase.
We're in the **"AI is raising the bar"** phase.

If you're serious about building great products, you need both:

- The vibes
- And the fundamentals

Let's not pretend vibes can do everything.
Let's build with eyes open.
Let's keep our hands on the keyboard.

Because the last 20% of engineering?

That's where the magic lives.

![graph-diminishing-returns]({{ site.baseurl }}/assets/graph-diminishing-returns.gif)

