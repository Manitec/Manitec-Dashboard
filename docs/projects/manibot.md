# ManiBot

**What it is:** Joe's personal AI chatbot assistant with a custom sarcastic personality.

**Live URL:** [chat.manitec.pw](https://chat.manitec.pw)

**Blog Post:** [manitec.pw/blog/manibot](https://manitec.pw/blog/manibot)

## Stack

- **Framework:** Next.js 15 (App Router)
- **Hosting:** Vercel
- **AI Engine:** Groq API (fast inference)
- **AI Layer:** Vercel AI SDK v5
- **Database:** Neon (serverless Postgres — stores chat history)

## Features (Live ✅)

- Multi-session sidebar — view and resume past conversations
- Persistent chat history saved to Neon DB
- Custom system prompt — sarcastic personality, knows who Joe is
- Fully deployed and public-facing

## Known Bugs

- Input box clips slightly on some screen sizes
- Returning to old sessions doesn't always restore messages correctly

## Next Steps

- [ ] Fix layout clip bug
- [ ] Fix session restore
- [ ] Add web search capability
- [ ] Give it GitHub access
- [ ] Build a private Joe-only version with deeper personality
- [ ] Explore GenX Router as Groq replacement for multi-model access

## Lessons Learned

- Next.js 15 — `params` is now a Promise, must `await` it
- AI SDK v5 — dropped `content` field, now uses `parts[]` array
- Git merge conflicts across 6 files simultaneously is a special kind of hell

!!! tip "Screenshot Needed"
    Drop a screenshot of [chat.manitec.pw](https://chat.manitec.pw) on [postimg.cc](https://postimg.cc/files) and I'll wire it in 📸
