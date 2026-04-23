# 2 Sigma Learning

[中文说明](README-zh.md)

Learn any field with a local AI tutor that teaches one chunk at a time, checks mastery, and keeps a record of what actually worked.

2 Sigma Learning is a Claude Code skill for people who want a real course instead of a one-off answer. Start it with `/2-sigma-learning`, and it runs a file-backed learning loop in the current folder: plan the course, teach in chunks, test retrieval, record evidence, and adapt the next class.

## Why this exists

In the 1980s, Benjamin Bloom described what became known as the **2 Sigma problem**: with the right learning conditions, one student can outperform 98% of peers. The two conditions were simple to name and hard to afford:

1. **One-to-one tutoring**  
   One teacher, one student, with the pace adjusted in real time.
2. **Mastery learning**  
   You do not move on because the chapter ended. You move on because you actually understand the material, usually at roughly 80% to 90% mastery.

That combination was historically expensive. It favored students who could afford sustained personal attention. Everyone else had to follow the pace of a classroom, even when they were already lost.

AI changes the economics. A local agent can now reproduce much of that loop at very low cost. But ordinary AI chat still fails in unfamiliar fields, because beginners often do not know what to ask. Broad answers are not the same thing as learning.

What helps is a tutor that asks *you* questions:

- What are you trying to learn?
- What do you already know?
- Can you explain this idea back to me?
- Are you ready to move on, or do you need a different explanation?

That is the job of this skill.

## What this does

Use `2-sigma-learning` when you want Claude Code to run a persistent course, not just a conversation.

It can:

- start a new course from an empty folder
- continue a course from `proposal.md` and existing class files
- teach one chunk at a time instead of dumping a full lesson
- ask 1–2 checkpoint questions after each chunk
- use warm-up review based on weak carryover concepts
- gate progression at roughly 80% to 90% mastery
- switch explanation routes when you are stuck
- write learning records back to local files
- generate `summary.md` when the course is done

## How to start

Invoke it only with the slash command:

```text
/2-sigma-learning
```

Then say what you want to learn, or say that you want to continue an existing course in the current folder.

If the folder already contains `proposal.md`, the skill defaults to continuing. If the folder is empty, it defaults to starting a new course. If the folder contains unrelated files, it can propose a subfolder such as `./courses/<slug>/`.

## What it asks from you

When starting a new course, it asks only for the information needed to draft a useful plan:

- your learning goal
- your current background and weak spots
- your time preference
- your target depth
- whether to use general knowledge or your own sources

Then it drafts `proposal.md`, shows it to you, and iterates until the class sequence makes sense.

During teaching, it does not keep talking forever. It teaches one chunk, asks 1–2 checkpoint questions, evaluates your answer, and decides whether to continue, review, or switch explanation routes.

## What it writes

A course lives in local files. The default shape is:

```text
proposal.md
Class 01 - <topic>.md
Class 02 - <topic>.md
...
summary.md
```

`proposal.md` holds the course plan, class sequence, progress, and weak concepts that should return in future warm-up review.

Each class file holds the class goal, warm-up review, textbook chunks, checkpoint questions, exercises, the class rubric, and a `## Learning Record` section.

At the end of a class, the skill writes back:

- what was covered
- the checkpoint questions
- your answers
- the feedback given
- mastery estimates
- remaining gaps
- explanations or analogies that helped
- what should happen next

When the course is complete, it generates `summary.md` with mastered concepts, residual weak points, and recommended next directions.

## Why local files matter

A tutoring loop needs memory. A normal chat window loses too much context when the session ends.

A local agent can keep track of:

- what you already understand
- which misconceptions keep recurring
- which explanations failed
- which explanation finally worked
- which weak concepts should return in the next warm-up

That is the difference between generic AI help and a course that adapts to you over time.

## Use it for

This skill is a good fit when you want to:

- learn a new field from zero without staring at a blank input box
- turn a broad topic into a class-by-class plan
- study from your own textbooks, papers, or docs
- keep a persistent learning record across sessions
- force yourself into retrieval practice instead of passive reading

## Limits

This is a learning workflow, not a credential.

- It does not replace accredited teaching, supervision, or domain experts.
- For medical, legal, financial, safety, or other high-stakes domains, verify important claims with authoritative sources.
- The mastery estimate is a working teaching judgment, not a formal exam score.
- The skill only runs when you explicitly invoke `/2-sigma-learning`.

## Skill file

The execution rules live in [SKILL.md](SKILL.md).
