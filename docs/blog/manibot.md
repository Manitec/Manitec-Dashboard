# I Built an AI Chatbot From Scratch This Weekend

*April 3, 2026 &middot; Joe &middot; Dev Log &middot; ~7 min read*

> Also published at [manitec.pw/blog/manibot](https://manitec.pw/blog/manibot/)

---

## (It Did Not Go Smoothly)

If you're new here — I'm Joe. I run a one-man operation called Manitec out of the hills of Tennessee. No team, no funding, no formal education. Just a laptop, too many browser tabs, and a stubborn refusal to quit.

This weekend I upgraded ManiBot — my personal AI assistant that lives at [chat.manitec.pw](https://chat.manitec.pw) — from a basic chatbot into something that actually feels like a real product. Multiple chat sessions, persistent memory saved to a real database, and a personality that will roast you to your face.

It took eight failed deployments to get there. Here's how it went.

---

## What I Was Building

ManiBot started as a simple AI chat interface. You type, it responds, you refresh the page and it forgets you ever existed. Useful, but not impressive.

The goal this weekend was to fix that. I wanted:

- A sidebar showing your past conversations
- Chat history that actually saves — so when you come back tomorrow, it remembers
- A real personality instead of the default "Hello! How can I assist you today?" energy

Simple enough on paper. Chaos in practice.

---

## The Stack

Here's what ManiBot runs on:

- **Next.js 15** — the framework everything is built in
- **Vercel** — where it's deployed and hosted
- **Groq API** — the AI engine powering the responses (insanely fast)
- **AI SDK v5** — the layer that connects the AI to the app
- **Neon** — a serverless Postgres database that stores chat history

I didn't pick these because they're trendy. I picked them because they're free at my scale and they work. When you're building solo with no budget, free and functional beats fancy every time.

---

## What Actually Happened

Here's the part nobody puts in their tutorials.

I started the session with six files simultaneously stuck in git merge conflicts. Not one. Six. Every file I tried to open had the `<<<<<<< HEAD` markers that mean git has no idea what version of reality is correct. So before I could write a single line of new code, I had to manually clean up six files and push them back to GitHub one by one.

That was just the warm-up.

**Problem 1: Next.js 15 changed how route parameters work.**
In previous versions you could grab URL parameters like `params.id` and go. In version 15 they made params a Promise — meaning you have to `await` them first. There's no big warning about this. You just get a cryptic type error and spend time figuring out why something that worked before suddenly doesn't.

**Problem 2: AI SDK v5 removed the `content` field from messages.**
The previous version stored message text in a simple `content` field. Version 5 replaced it with a `parts` array — a more flexible structure but a breaking change that caught me completely off guard. Every place in my code that read `message.content` was now broken. I had to write a helper function to extract text from the new format.

**Problem 3: The layout wouldn't stay inside the screen.**
After getting the database working, the input box at the bottom of the chat kept getting clipped by the browser. I pushed three separate fixes before it behaved. Flexbox is a blessing and a curse.

Eight deployments. Eight build logs. Eight chances to give up.

---

## The Moment It Worked

When the sidebar showed "hello mani" as the first saved session — a real conversation title pulled from a real database — I actually felt something. That's the moment a project stops being a prototype and starts being a product.

Then I tested the personality.

I asked ManiBot *"who is Joe?"* and it said:

!!! quote ""
    "Joe's the stubborn bastard who built me at 2am instead of sleeping like a normal human. Tennessee hillbilly turned solo developer, thinks too much about philosophy and not enough about business models. Keeps starting ridiculous projects like I'm supposed to fix his chaotic life."

That's when I knew it was done. 😂

---

## What's Next

ManiBot still has bugs. The input box clips slightly on some screens. When you return to an old conversation, your messages don't always restore correctly. I know about them. I'll fix them.

Beyond that I'm planning to add web search, give it access to my GitHub, and eventually build a private version just for me with a completely different personality. If you want to follow that journey, you're in the right place.

---

## The Real Point

I built this with no budget, no team, and no computer science degree. I failed English four times. I quit high school just before I turned seventeen.

None of that stopped me from shipping a real AI product this weekend.

You don't need permission. You don't need credentials. You just need to start, tolerate the failures, and keep pushing commits until the build goes green.

ManiBot is live at [chat.manitec.pw](https://chat.manitec.pw). Go break it. 🖤

---

*Built by Joe — [Manitec.pw](https://manitec.pw)*

[Back to Blog](index.md) | [Home](../index.md)
