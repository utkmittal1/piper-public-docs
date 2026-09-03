# Piper documentation

This is the end-user documentation for Piper, built as a Mintlify MDX site. It
is written for a non-technical knowledge worker: a product manager, a
salesperson, a marketer, an analyst, a founder. They know their job and they do
not know code, so no page sends them to a terminal, a config file, or a
low-level setting. Every page points at Piper's own interface instead. Piper also
reads these pages to explain itself, so each one is written tightly enough that
quoting a line cannot produce a false claim.

## Preview it locally

The Mintlify CLI ships as the `mint` package.

```bash
npm i -g mint          # install the CLI
cd piper-docs          # the folder holding docs.json
mint dev               # serves the site at http://localhost:3000
```

Two more worth knowing:

```bash
mint broken-links      # checks every internal link resolves
mint update            # upgrades the CLI itself
```

`mint dev` reloads as you save, so leave it running while you edit.

## Deploy it

Mintlify deploys from a connected GitHub repository. Push this folder to a repo,
connect it in the Mintlify dashboard, and every push to the production branch
triggers a build. There is no deploy command to run.

Run `mint broken-links` before you push. It is the one check that catches a
renamed page before a reader does.

## What the site holds

Thirty-two pages in eight sections, plus seven diagrams. `docs.json` is the
navigation and the theme, and it matches the files on disk exactly: every page
appears once and resolves to a real `.mdx`.

| Section | Folder | Pages |
|---|---|---|
| Getting started | `getting-started/` | Overview, Set up Piper, Your first task |
| Core concepts | `concepts/` | How Piper works, Sessions and the workspace, Projects, AI providers |
| What Piper knows about you | `context/` | Memory, Instructions and profile, Response style, Knowledge Sources |
| Connecting your tools | `connections/` | Connecting your tools, Integrations, Secrets, Web and sign-ins |
| Working with Piper | `working/` | Describing what you need, Reviewing results, Files and deliverables, Skills, Tools, Notifications, Appearance |
| Piper on its own | `autonomous/` | Chief of Stuff, Autonomous tasks, Long-running tasks, Custom agents |
| Staying in control | `control/` | Your data stays local, Approvals and permissions, The sandbox |
| Reference | `reference/` | Integrations catalog, Keyboard shortcuts, Troubleshooting and FAQ |

The seven diagrams live in `images/diagrams/` as SVG: `core-loop.svg`,
`session-workspace.svg`, `memory-levels.svg`, `ai-provider-context.svg`,
`chief-of-stuff-flow.svg`, `long-running-task.svg`, and `sandbox.svg`. Each one
is embedded on exactly one page. There are no screenshots anywhere, which is
deliberate. A screenshot goes stale the moment the UI moves.

## How these pages were built, and the bar to hold

**The Piper code is the only source of truth.** Not the brand doc, not the style
guide, not anyone's memory of the product. Every feature, on-screen label, path,
number, and claim on these pages traces to a line of code. A claim that could not
be grounded was cut or recorded as an open question, never guessed at. Several
briefs turned out to be wrong and the code won each time.

Each page was drafted from the code, then audited against it a second time by
someone who had not written the draft, then given a separate language pass. The
findings, the code evidence behind each rewrite, and every unresolved question
are recorded in `docs-audit-log.md`, kept beside this folder.

**The brand doc and the style guide govern how the writing reads, never what a
feature is.** Voice, tone, naming, and rhythm come from them. Facts do not.

If you edit a page, hold the same bar. Open the code, quote the real string, and
cut anything you cannot point at.

## Two conventions worth knowing before you edit

**"AI provider" is the name for the service that does Piper's thinking.** The
pages never call it an engine, a runtime, an LLM provider, or bare AI. The app's
own Settings item still reads **Agent Runtime**, so the docs and the interface
disagree on this one label. That is deliberate and recorded in the audit log.

**Five labels the pages quote in sentence case render uppercase in the app**,
because `globals.css` applies `text-transform: uppercase`: **Execution plan**,
**Step 3 of 5**, **Approval needed**, **Auto-denied**, and **Artifacts**. Every
page uses the code's own capitalization rather than shouting.

## One diagram limit worth knowing

The SVGs switch colour with the reader's **system** colour scheme, not with
Mintlify's own dark-mode toggle. A reader on a light Mac who flips the docs to
dark gets a dark page with light diagrams. Nothing breaks and everything stays
legible, but the two do not match.

The cause is that each diagram loads through an `img` tag, and a file loaded that
way cannot see the theme class Mintlify puts on the page. The SVGs switch on a
`@media (prefers-color-scheme: dark)` block instead.
