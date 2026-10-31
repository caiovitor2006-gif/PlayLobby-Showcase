# PlayLobby — Product & QA Case Studies

**A few concrete examples of how I approach multiplayer products, debugging, testing, and iterative improvement.**

[← Back to the PlayLobby Showcase](../README.md) · [Visit the live platform](https://playlobby.online)

> **Context:** PlayLobby is an active web-based collection of multiplayer party games. These are retrospective examples grounded in development test files and checkpoint notes. They describe work undertaken and results reported at those checkpoints—not independently audited, continuously monitored production metrics. The underlying source repositories remain private.

---

## Case 1 — Scribble: a layout regression caused by browser resizing

**Product problem.** In the multiplayer word-building game **Scribble**, changing the browser zoom or resizing the viewport could leave the game board incorrectly sized. A layout that looked fine initially could become misaligned after the browser finished reflowing.

**Investigation and approach.** The issue involved fitting the board during an intermediate browser layout state. A change was made to allow an immediate board fit and then a second, settled fit after the resize. The workflow combined observing the issue in the browser, identifying repeatable triggers, and checking that the correction did not undo the approved layout.

**Verification recorded.** A regression test in the private source checks that the board resize behavior includes both fitting stages and that the relevant viewport resize events schedule them. The test captures an important behavioral contract; by itself it is not a substitute for visual checks across real browsers and devices.

**What this demonstrates:** UI regression analysis, reproducible bug reports, testable acceptance criteria, and attention to real user environments.

[See the Scribble interface](../screenshots/scribble.png) · [Open Scribble](https://scribble.playlobby.online/)

## Case 2 — Chameleon 2D: validating a full multiplayer journey

**Product problem.** A multiplayer game must remain consistent across players, not just render correctly in one browser. Joining, starting, progressing through rounds, scoring, disconnecting, and changing room ownership all create opportunities for errors.

**Test approach.** An early Chameleon 2D test report documents accelerated **two-client** local testing: one player creates a room, another joins, they play through the camouflage-and-hunt flow, the server evaluates hits and misses, scores are calculated, rounds advance, and the session returns to the lobby. Separate checks cover reconnection and room-management rules.

**Verification recorded.** The report marks the local two-client, reconnection, and room-authority checks as passed. It explicitly leaves graphical browser QA, touch-device checks, deployment, and production routing for later gates. This distinction matters: a local passing test is evidence of that scenario, **not** proof that every live environment is bug-free.

**What this demonstrates:** scenario-based multiplayer QA, state-transition testing, edge-case awareness, and honest reporting of coverage gaps.

[See the Chameleon 2D interface](../screenshots/chameleon-2d.png) · [Open Chameleon 2D](https://chameleon2d.playlobby.online/)

## Case 3 — Acromaniacs: improving performance without changing gameplay

**Product problem.** Large interface assets make a web game heavier to load, even when the gameplay itself is simple. Performance work also introduces a risk of broken images or stale browser caches.

**Improvement.** A documented Acromaniacs interface update converted **six image assets from PNG to WebP**, preserving their visual layout while adjusting asset references and cache handling. The release plan deliberately kept game rules, scoring, rooms, and round flow outside the change scope.

**Measured result in the development report:**

| Metric | Before | After |
| --- | ---: | ---: |
| Combined size of six interface images | 8,333,042 bytes | 828,568 bytes |

That is **approximately 90% less image data** for those six assets, not a measured 90% improvement to the whole site's loading time. The project report also records passing HTTP/cache production checks for that release checkpoint.

**What this demonstrates:** measurable performance optimization, change-scope discipline, release verification, and awareness of regression risks.

[See the Acromaniacs interface](../screenshots/acromaniacs.png) · [Open Acromaniacs](https://acromaniacs.playlobby.online/)

---

## How I work with AI-assisted development

I use AI coding assistance as part of the development process, while concentrating on the product and verification loop:

1. **Define expected behavior:** what users should see, do, and experience together.
2. **Make problems reproducible:** write down the steps, environment, actual behavior, and desired result.
3. **Review proposed fixes:** check that a change addresses the original issue without disrupting other behavior.
4. **Test again:** use appropriate automated checks, manual browser testing, and multiplayer scenarios.
5. **Communicate limits:** separate confirmed observations from assumptions, unverified paths, and future release gates.

This is a **hands-on, AI-assisted workflow**, not a claim that I independently wrote every part of the application or personally executed every automated test documented here.

## Scope and evidence

These examples were selected from private project development materials because they demonstrate general product and QA work **without disclosing application source, operational details, private user data, or credentials**. The public screenshots show interfaces and lobbies; they are not presented as recordings of the test sessions above.

**Interested in practical product support or QA work?** [Visit my GitHub profile](https://github.com/caiovitor2006-gif) to see other projects and contact options.
