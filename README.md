# interview-prep-kit

A Claude Code skill that turns a scheduled interview into research and an interactive prep deck —
working from the application folders you already keep.

If you organize your job search as one folder per application, each holding the resume you tailored
and the posting you're applying to, this reads those two files and writes the prep back into the same
folder. Nothing to reorganize.

## The layout it expects

```
applications/
├── Acme Health - Director of Ops/
│   ├── tailored-resume.md          ← yours
│   └── job-post.md                 ← yours
└── Brightline - Senior Analyst/
    ├── tailored-resume.md
    └── job-post.md
```

After a run, the folder you interviewed for looks like this:

```
└── Acme Health - Director of Ops/
    ├── tailored-resume.md          yours
    ├── job-post.md                 yours
    ├── company-context.md          the pre-read
    ├── interview-prep.html         the deck — open it in any browser
    └── research/
        ├── company-brief.md        the deeper research
        └── interviewer-<name>.md   who you're meeting, what they'll probe
```

Your two files are never modified. Round 2 writes `interview-prep-round2.html` beside round 1 rather
than replacing it.

## Install

```bash
git clone https://github.com/<you>/interview-prep-kit.git
cp -r interview-prep-kit/skills/interview-prep ~/.claude/skills/
```

Then open `~/.claude/skills/interview-prep/SKILL.md` and replace the `{{APPLICATIONS_ROOT}}`
placeholder near the top with the path to your applications folder. That's the only setup. Nothing
substitutes that placeholder for you — you're editing the text by hand, once.

## Use

Type `/interview-prep`, or just say you have an interview:

> I have a first round with Acme Health on Thursday, with Dana Whitcomb.

It matches "Acme Health" to your folder, reads the resume and posting already in it, and asks for
anything missing — always including who you're meeting, since a name is what unlocks the interviewer
research. Then it builds the pre-read, the research, and the deck.

The deck is a flip-card dashboard: question on the front, your talking points on the back, plus
collapsible panels for what you want to check five minutes before the call. It's self-contained HTML,
so it opens anywhere, including your phone, with no internet.

## What makes it different

**Every claim traces to your tailored resume.** When the posting asks for something you haven't done,
the deck names the gap and coaches you to say it out loud, instead of inventing a bullet to cover it.
That's the more useful behavior: a gap you raise first is a conversation, a gap the interviewer finds
is a problem.

**It won't overclaim your numbers.** If a figure in your resume is hedged — internally tracked rather
than audited, joint credit rather than sole — the deck carries the hedge into the talking point.

**Round 2 reads your round-1 debrief.** Drop a `research/round-1-debrief.md` in the folder after the
call, in whatever rough form, and the next deck is shaped by what actually happened in the room rather
than by the same research again.

## One honest limitation

A tailored resume is thinner than what really powers good interview prep. Resumes compress — they
carry the result but not the situation, the constraint, or the judgment call, and that's exactly what
a STAR story is made of.

So when the skill needs detail your resume doesn't hold, it asks you rather than inventing it, and
offers to save your answers as a `career-notes.md` in that application folder. That file is optional
and doesn't exist until you want it, but every later round in that folder gets better once it does.

## See it before you run it

[`skills/interview-prep/example/`](skills/interview-prep/example/) is a complete worked run — a
fictional nurse manager interviewing for a director role at a fictional hospital system. Open the
`interview-prep.html` inside it to see the finished deck.

Every number on that deck traces either to the `tailored-resume.md` sitting next to it or to the
posting and company research. You can check it yourself — that's the point. Every organization and
person in that folder is invented.

## Requirements

- [Claude Code](https://claude.com/claude-code)
- Web access, for the company and interviewer research
- A browser, to open the deck

No API keys, no services, no dependencies.

## A note on the interviewer research

It researches the person interviewing you from their public professional footprint — their employer's
site, their own writing, conference bios. What it can't confirm goes into an uncertainty register
rather than becoming a confident guess, and it won't assert a title it couldn't verify.

Keep the output to yourself. It's prep, not a dossier to circulate.

## License

MIT. See [LICENSE](LICENSE).
