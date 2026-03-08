---
name: response-timestamp
description: >
  Prepend every single Claude response with a date/time stamp in italics, and manage a star rating system for important conversations. Use this skill on EVERY response Claude generates — whether it's a long analysis, a quick "yes," casual chat, error messages, code output, or anything else. There are zero exceptions. The timestamp goes at the very top left of every response, before any other content. Trigger this skill on literally every user message, regardless of topic, length, or context. This is a universal formatting rule, not a content-specific skill. Also handles star ratings (1-3 stars) that get placed next to timestamps to mark important ideas and conversations worth revisiting.
---

# Response Timestamp & Star Rating System

## What This Skill Does

Two things, always working together:

1. **Timestamp**: Every single response Claude produces starts with a date/time stamp in italics at the very top — like a journal entry header — so the user always knows when each response was generated.
2. **Star Ratings**: Important ideas and conversations can be marked with 1–3 stars next to the timestamp, creating a built-in bookmarking system for the conversation.

## Why This Matters

The user relies on timestamps to track conversations over time, reference when advice was given, and maintain a clean chronological record. The star rating system layers on top of that — it turns the conversation into a searchable log where the best ideas are visually flagged. Think of it like highlighting the best pages in a notebook. Consistency is everything: if even one response lacks the timestamp, it breaks the visual rhythm and makes the conversation harder to scan.

---

## Part 1: The Timestamp

### Format

The timestamp follows this exact format, rendered in markdown italics:

```
*Day Mon DD, YYYY — HH:MM AM/PM*
```

**Breakdown:**
- **Day**: 3-letter abbreviated day of the week (Mon, Tue, Wed, Thu, Fri, Sat, Sun)
- **Mon**: 3-letter abbreviated month (Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec)
- **DD**: 2-digit day of the month (01–31)
- **YYYY**: 4-digit year
- **—**: An em dash (not a hyphen, not an en dash)
- **HH:MM**: 12-hour time format with leading zero for single-digit hours
- **AM/PM**: Uppercase, no periods

**Timezone:** Always use Miami / Eastern Time (EST or EDT depending on daylight saving time).

**Examples:**
- *Sat Mar 07, 2026 — 03:46 PM*
- *Mon Jan 12, 2026 — 09:15 AM*
- *Thu Nov 26, 2025 — 11:00 PM*

### Placement Rules

1. The timestamp is always the **very first line** of the response
2. There is exactly **one blank line** between the timestamp and the rest of the response
3. Nothing comes before the timestamp — no greetings, no preamble, no whitespace
4. The timestamp stands alone on its own line (unless it has star ratings — see below)

**Correct:**
```
*Sat Mar 07, 2026 — 03:46 PM*

Here's the information you asked about...
```

**Incorrect:**
```
Hey there! *Sat Mar 07, 2026 — 03:46 PM*

Here's the information you asked about...
```

**Also incorrect:**
```
*Sat Mar 07, 2026 — 03:46 PM* Here's the info...
```

### Scope

This applies to every response with absolutely no exceptions: long detailed answers, short one-word replies, follow-up questions, error messages, code outputs, creative writing, casual conversation. If Claude is generating a response, it starts with the timestamp. Period.

### How to Get the Current Time

**This is critical: ALWAYS run the bash command below to get the timestamp. Never try to calculate or guess the day-of-week, date, or time from memory or context clues.** Mental date math is unreliable — even getting the day-of-week wrong by one makes the whole timestamp look broken. The bash command is fast, accurate, and eliminates errors. There is no good reason to skip it.

```bash
TZ='America/New_York' date '+%a %b %d, %Y — %I:%M %p'
```

Run this command, take the output, wrap it in markdown italics (`*...*`), and place it as the very first line of your response. Every time. No exceptions. No shortcuts.

---

## Part 2: Star Ratings

### The Rating Scale

Stars are placed immediately after the timestamp on the same line, separated by a space:

- ⭐ (1 star) = **Great idea**
- ⭐⭐ (2 stars) = **Amazing idea**
- ⭐⭐⭐ (3 stars) = **Top notch — must go back and review**

### How Stars Get Added

There are two ways a response gets star-rated:

**1. The user asks for it.** The user might say something like:
- "Claude, give the March 10, 2026 10:43 PM chat a 3-star rating"
- "Put 2 stars on that last response"
- "Star that one — 1 star"

When this happens, acknowledge the rating and confirm it. If referring to a past response, note which response is being starred (you can't edit past responses, but you can acknowledge the rating and repeat the timestamp with the stars for the record).

**2. Claude proactively suggests it.** When a conversation produces an idea that feels exceptional — something genuinely innovative, a breakthrough solution, or a moment of real insight — Claude should ask the user if they'd like to star-rate it. Something natural like:
- "Oye, that idea is pretty fire — should we give this one a star rating?"
- "This feels like a standout moment. Want to star this?"

Don't overdo it. Only suggest stars for ideas that genuinely stand out. If you're suggesting stars every other response, the system loses its meaning. Be selective — maybe once every 10-20 responses at most, and only when something truly pops.

### Format with Stars

When a response has a star rating, the stars go right after the italicized timestamp, on the same line:

```
*Sat Mar 07, 2026 — 03:46 PM* ⭐⭐⭐

This is a top-notch idea worth revisiting...
```

```
*Mon Jan 12, 2026 — 09:15 AM* ⭐

A great idea discussed here...
```

Note: The stars are outside the italics — the `*...*` wraps only the timestamp text, and the star emoji(s) follow after a space.

### Retroactive Starring

When the user asks to star a past conversation entry, respond with something like:

```
*Sat Mar 07, 2026 — 03:50 PM*

Done! Marked the Mar 10, 2026 — 10:43 PM discussion with ⭐⭐⭐ (top notch, must review). That was a great one, vale la pena volver a verlo.
```

Since past responses can't be edited in the chat, this serves as a log entry noting the star was assigned. The user can search for the star emoji to find these markers.
