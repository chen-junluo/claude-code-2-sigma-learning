# 2 Sigma Learning

[中文说明](README-zh.md)

Learn any field with a local AI tutor that teaches in small chunks, tests mastery, and can resume from disk even after the chat is gone.

2 Sigma Learning is a Claude Code skill for people who want a real course instead of a one-off answer. Start it only with `/2-sigma-learning`, and it runs a file-backed learning loop in the current folder: plan the course, teach one chunk, test retrieval, record evidence, and adapt the next class.

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
- recover teaching state by reading the files on disk, not by trusting chat memory
- teach one chunk at a time instead of dumping a full lesson
- ask 1–2 checkpoint questions after each chunk
- use warm-up review based on weak carryover concepts
- gate progression at roughly 80% to 90% mastery
- switch to a different explanation route when you are stuck
- create remediation classes such as `Class 02b - <topic> (remediation).md`
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

During teaching, it does not keep talking forever. It teaches one chunk, asks 1–2 checkpoint questions, evaluates your answer, and decides whether to continue, review, ask a harder question, or switch explanation routes.

## What it writes

A course lives in local files. The default shape is:

```text
proposal.md
Class 01 - <topic>.md
Class 02 - <topic>.md
Class 02b - <topic> (remediation).md
...
summary.md
```

`proposal.md` is the course-level index. It holds the learning goal, knowledge map, class sequence, progress, weak concepts carryover, and update log.

Each class file is the class-level evidence file. It holds the lesson content and the record needed for a future session to continue teaching without guessing.

Class files use fixed English structural headings, even when the teaching content is in another language. This keeps the files easy to read and easy for the skill to parse across sessions. Important sections include:

- `## At a Glance`
- `## Key Takeaways`
- `## Textbook`
- `## Misconceptions / Weak Concepts`
- `## Learning Record`
- `## Mastery & Gaps`
- `## Hooks for Next Class`

At the end of a class, the skill runs a four-step close:

1. write or update the class file with real evidence from the session
2. update `proposal.md` with progress and weak carryover concepts
3. scaffold the next class or a remediation class
4. ask whether to continue now or stop here

The skill must not fabricate textbook content, worked examples, user answers, or learning records. If the next class is not ready yet, it creates a skeleton instead of inventing a lesson.

## Why local files matter

A tutoring loop needs memory. A normal chat window loses too much context when the session ends.

Version 2 of this skill is built around one constraint: a fresh session with no chat memory should be able to resume teaching by reading only the files on disk.

That means the files must preserve:

- what you already understand
- which misconceptions keep recurring
- which explanation route failed
- which explanation finally worked
- which weak concepts should return in the next warm-up
- what the next class should open with

That is the difference between generic AI help and a course that adapts to you over time.

## How it adapts when you are stuck

The skill does not just repeat the same explanation with different wording.

When a core concept falls below 60% mastery, it must switch to a different explanation route:

1. abstract or formal definition
2. concrete example
3. analogy
4. counterexample or contrast
5. visual or structural explanation
6. prerequisite drop-down

It also records which route worked, so the next session can reuse useful framings and avoid failed ones.

## Use it for

This skill is a good fit when you want to:

- learn a new field from zero without staring at a blank input box
- turn a broad topic into a class-by-class plan
- study from your own textbooks, papers, or docs
- keep a persistent learning record across sessions
- force yourself into retrieval practice instead of passive reading
- repair weak concepts before moving on

## Limits

This is a learning workflow, not a credential.

- It does not replace accredited teaching, supervision, or domain experts.
- For medical, legal, financial, safety, or other high-stakes domains, verify important claims with authoritative sources.
- The mastery estimate is a working teaching judgment, not a formal exam score.
- The skill only runs when you explicitly invoke `/2-sigma-learning`.

## Skill file

The execution rules live in [SKILL.md](SKILL.md).
