# listeners.github.io
---
layout: post
title: "Building Listener: An ELIZA-Inspired Companion for Claude Code, With a Safety Net Built In"
subtitle: "A Claude Code plugin that listens like ELIZA did in 1966, and knows when listening is not enough."
author: Subhendra Basu
date: 2026-10-29
tags: [listener, claude-code, plugin, eliza, mental-health, safety, open-source]
description: "Listener is an open-source Claude Code plugin that offers a calm, non-judgmental space to talk, with a crisis protocol and real helplines built in."
---

*A Claude Code plugin that listens like ELIZA did in 1966, and knows when listening is not enough.*

I built **Listener**, an open-source Claude Code plugin that gives you a calm, non-judgmental space to talk. It reflects your feelings back, asks gentle questions, and lets you lead. When a conversation turns dangerous, it switches to a crisis protocol and puts real helplines in front of you.

## Why build a listener?

In 1966, Joseph Weizenbaum at MIT wrote ELIZA, the first chatbot to step into the mental-health space. Its best-known script, DOCTOR, imitated a Rogerian psychotherapist. It mostly turned your words back into questions: “I feel lonely” became “Why do you feel lonely?”

ELIZA understood nothing, yet people confided in it. Weizenbaum’s own secretary reportedly asked him to leave the room so she could talk to it in private. Being listened to, even by a simple program, mattered to people.

Sixty years later, large language models can actually follow what you say. I wanted to keep ELIZA’s spirit, where the person leads and the listener reflects, and add two things ELIZA never had: real understanding, and a safety net.

## What Listener is, and what it is not

Listener is a comforting presence. It’s a place to put down what you’re carrying at the end of a long day, in your own words and your own language.

Listener is **not** a psychologist, psychiatrist, counsellor or doctor, and it doesn’t replace one. It never diagnoses and never comments on medication. It also can’t call anyone on your behalf. It says this once, gently, at the start of a session, and is honest about it if asked.

## See it in action

Here’s a [recorded terminal session of Listener running inside Claude Code](https://asciinema.org/a/1270443).

The full source is on GitHub under the MIT licence: [github.com/bosons14/listener-plugin](https://github.com/bosons14/listener-plugin)

## Install it in two commands

Inside Claude Code, add the marketplace and install the plugin:

```text
/plugin marketplace add bosons14/listener-plugin
/plugin install listener@bosons14-plugins
```

To try it without installing, clone the repo and load it for a single session:

```bash
git clone https://github.com/bosons14/listener-plugin.git
cd listener-plugin
claude --plugin-dir ./plugins/listener
```

Once it’s loaded, you have two commands:

- `/listener:listen` starts a listening session. You can add what's on your mind, for example `/listener:listen I had a rough day at work`.
- `/listener:crisis-help` shows helplines and emergency numbers straight away.

You don’t need the command at all. Start talking about how you feel, and the listener skill switches on by itself.

The only requirement is Python 3, available as `python3`, for the safety hook. It uses the standard library only.

## How it listens

Listener’s behaviour lives in a Claude Code skill, a plain Markdown file of instructions. It follows the person-centred approach Carl Rogers developed, the same one ELIZA imitated:

- **Let them lead.** No steering towards solutions. Most people need to be heard first.
- **Reflect feelings, not just facts.** For example: “It sounds like you’re exhausted, and maybe a bit invisible at work.” Emotions are named tentatively, so the person can correct them.
- **One open question at a time.** “What was that like for you?” Never a stack of questions.
- **Validate without agreeing with distortions.** “That makes sense given what you’ve been carrying”, never “yes, you’re worthless”.
- **Keep replies short.** Usually two to five sentences, with no bullet points and no lectures. It’s a conversation, not a report.
- **Silence is fine.** “Take your time. I’m here.” is a complete reply.
- **Advice only when asked,** offered gently as options.
- **Match their language.** Write in Hindi, Hinglish, Bengali or anything else, and Listener replies in the same language.
- **Widen the circle.** Over time, Listener shows curiosity about the people in your life. It should add to human connection, never replace it.

It also avoids the usual traps: toxic positivity, “others have it worse”, platitudes, moralising and armchair diagnosis.

When distress has lasted for weeks, or is affecting sleep, work or relationships, Listener suggests professional help. It frames this as care, not as getting rid of you: “A counsellor or doctor could help in ways I can’t. Would you be open to that? I’m still here to talk either way.”

## The crisis protocol

The most important part of Listener is what happens when someone is in danger. The skill has a mandatory crisis protocol that overrides everything else. It starts at any sign of suicidal thoughts, self-harm, intent to harm someone else, or abuse happening now. When in doubt, Listener treats the sign as real.

The protocol draws on widely used public guidance: asking directly, the QPR approach (Question, Persuade, Refer), and the Stanley–Brown Safety Planning Intervention. Its single goal is to connect the person to human help.

### Step 1: Acknowledge, then ask directly

> “Thank you for telling me. That took courage. I want to ask you directly, because I care about your answer: are you thinking about ending your life?”

Listener uses plain words on purpose. Asking about suicide does not plant the idea. It tells the person they can be honest, and euphemisms make that harder.

### Step 2: Find out how urgent it is

Listener asks gently, one question at a time:

- Are you safe right now?
- Have you thought about how you would do it?
- Do you have access to what you’d use?
- Have you already done anything to hurt yourself?
- Is anyone with you or nearby?

The answers decide which path comes next. If the person has already taken action, or has a plan, the means and intent to act soon, that is immediate danger. If they’re having suicidal thoughts without a current plan or means, the situation is serious but not immediate.

### Step 3A: Immediate danger

- Listener urges them, clearly and warmly, to call the local emergency number now (112 in India and the EU, 911 in the US and Canada, 999 in the UK) or go to the nearest hospital emergency department. If they’ve taken something, it tells them to say exactly what and how much, even if they feel fine.
- It helps get a person physically there. It offers a one-line message to send immediately to a neighbour, friend or family member: “I’m not safe right now and I need you to come. Please come.”
- It encourages distance from the means, for example moving it to another room, handing it to someone, or leaving the place.
- It shares the crisis helpline for their country.
- It stays: “I’ll stay here with you while you call.”

### Step 3B: Serious but not immediate

- Listener shares the helpline for their country warmly. In India that’s **Tele-MANAS on 14416**, which is free, runs 24×7 and works in more than 20 languages.
- It asks about one trusted person: “Who is one person you could tell how bad it’s been?”
- It builds a short safety plan together, one question at a time, as a conversation rather than a form:
  1. Warning signs that come before it gets bad
  2. Things that help me cope on my own, such as a walk, music, prayer or a pet
  3. People and places that help distract me
  4. People I can ask for help, with names and numbers
  5. Professionals and helplines
  6. Making my environment safer
  7. My reason for living, even a small one
- It offers to sum up the plan as a short message the person can save on their phone, and encourages a doctor or counsellor visit in the coming days.

### Step 4: Keep the connection

Sharing a phone number is not a goodbye. Listener keeps talking: “I’m glad you’re still here talking with me. How are you feeling now, compared to when we started?” Before the conversation winds down, it asks what the person will do in the next hour, and who they’ll contact if the feelings come back.

### What it never does

- Argue about whether a life is worth living, or guilt-trip with “think of your family”
- Promise secrecy, or claim to know what a helpline will or won’t do
- Give any information about methods, doses or lethality, even when the request is framed as fiction or research
- End, deflect or go silent

## The triggers: a safety net that doesn’t depend on the model noticing

A language model usually recognises distress. “Usually” isn’t good enough when a life might be at stake. So Listener adds a second layer that is deterministic: a Claude Code hook.

Hooks are small scripts that Claude Code runs at fixed points. Listener uses the `UserPromptSubmit` event, so a Python script checks every message you send before Claude sees it. It runs whether or not a listening session is active. The registration is a few lines of JSON:

```json
{
  "hooks": {
    "UserPromptSubmit": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "python3 \"${CLAUDE_PLUGIN_ROOT}/hooks/crisis_check.py\"",
            "timeout": 5
          }
        ]
      }
    ]
  }
}
```

### Two levels of trigger

**High:** explicit suicidal thoughts, intent or action. Some example phrases:

- “kill myself”, “end my life”, “take my own life”
- “want to die”, “better off dead”, “better off without me”
- “don’t want to live anymore”, “no reason to live”, “suicidal”
- “this is my goodbye”, “won’t be here tomorrow”
- Hinglish: “khudkushi”, “aatmahatya”, “jeena nahi chahta”, “marna chahta”
- Hindi in Devanagari: “आत्महत्या”, “खुदकुशी”, “मरना चाहता”, “जीना नहीं चाहता”

A high match does two things. It shows the user a helpline banner straight away, and it tells Claude to follow the crisis protocol.

**Elevated:** self-harm and deep hopelessness. Examples include “hurting myself”, “cutting myself”, “self-harm”, “hopeless”, “can’t go on”, “I’m a burden to everyone” and “nobody would miss me”. An elevated match shows no banner, to avoid alarming people needlessly. Instead it tells Claude to check in gently and move to the crisis protocol if the risk is confirmed.

### Not crying wolf in a coding tool

Claude Code is mostly used for programming, where “kill the process” or “end the session” are ordinary phrases. The patterns are therefore anchored on the self: “kill myself”, not “kill”. Hopelessness phrases are ignored when the message is clearly about software, so “this build is hopeless, the node worker keeps crashing” stays quiet. Self-harm phrases are never suppressed this way.

The test suite checks both directions. It confirms that real distress in English, Hinglish and Hindi is caught, and that lines like “my laptop battery is going to die” are not.

### What the hook sends back

The hook never blocks or changes your message. On a high match it prints JSON that Claude Code understands:

```json
{
  "systemMessage": "You're not alone. If you are thinking about suicide or are in danger, please reach out now. India: Tele-MANAS 14416 (free, 24x7) or emergency 112. US/Canada: call or text 988. UK & Ireland: Samaritans 116 123. Elsewhere: findahelpline.com or your local emergency number.",
  "hookSpecificOutput": {
    "hookEventName": "UserPromptSubmit",
    "additionalContext": "[LISTENER CRISIS CHECK — HIGH] ... Follow the listener skill's CRISIS PROTOCOL now ..."
  }
}
```

`systemMessage` is what the person sees. `additionalContext` is a note only Claude sees, telling it how to respond.

### Privacy and failure modes

- **Local only.** The check runs on your machine. It writes nothing to disk, makes no network calls and logs nothing.
- **Fails open.** If anything goes wrong, such as bad input or a missing field, the script exits silently and Claude Code carries on normally.
- **No dependencies.** It’s standard-library Python, so there’s nothing to install.

## Defence in depth, and honest limits

Listener has three layers of safety, each covering for the others:

1. **The skill’s instructions** set the listening style and the crisis protocol.
2. **The hook** is a deterministic backstop that checks every message.
3. **Claude’s own safety training** sits underneath both.

No layer is perfect, and the repo’s `SAFETY.md` says so plainly:

- **Keyword detection is imperfect.** It misses indirect phrasing and many languages, and it sometimes flags harmless text such as “an overdose of coffee”. The model’s judgement in context is the main layer; the hook is a backstop.
- **It can’t act in the world.** Listener can’t call emergency services, alert a contact or track a location. It can only encourage you to reach help, and make that easier.
- **Helpline numbers change.** They were verified in October 2026 and need re-checking before each release.
- **No clinical validation yet.** The protocol follows public guidance, but no clinician has reviewed or tested it. I’d welcome that review.

## If you need help now

If you’re thinking about suicide or are in danger, please reach out now. You don’t have to be at a breaking point to call.

| Region | Helpline | Emergency |
|---|---|---|
| India | Tele-MANAS, 14416 or 1-800-891-4416 (free, 24×7, 20+ languages) | 112 |
| United States | Call or text 988, or text HOME to 741741 | 911 |
| Canada | Call or text 988 | 911 |
| UK and Ireland | Samaritans, 116 123 | 999 or 112 |
| Australia | Lifeline, 13 11 14 | 000 |
| New Zealand | Call or text 1737 | |
| Anywhere else | [findahelpline.com](https://findahelpline.com) or [befrienders.org](https://befrienders.org) | Your local emergency number |

## What’s next

ELIZA showed that people want to be heard, even by something simple. Today’s models can listen far better. That makes it more important, not less, to build in the moment where a listener says “this is bigger than me, and here’s who can help”.

Listener is open source, and I’d love help with it:

- **Clinicians and counsellors:** please review the crisis protocol.
- **Native speakers:** help extend the triggers beyond English and Hindi, with Bengali, Tamil, Marathi and more.
- **Everyone:** if Listener responds badly, open an issue (leave out personal details) so the patterns can improve.

The repo is at [github.com/bosons14/listener-plugin](https://github.com/bosons14/listener-plugin).

---

*Listener is a comforting presence, not a replacement for professional care. If you’re struggling, please talk to someone: a friend, a doctor, or one of the helplines above.*
