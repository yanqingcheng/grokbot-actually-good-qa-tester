---
name: what-is-testing
description: >-
  Read first, before any QA charter or test session, and whenever you're unsure
  whether something counts as a test finding or is worth raising. High-level
  explainer, in plain words, of what testing is and what a bug is.
---

*Version: 2026-10-22.r16.1 (pre-publication fixes: endings match step 10; r16: timebox is an upper limit: finish early once the mission is covered with evidence; stopping-heuristics credit).*
# What is testing

The ideas come from James Bach and Michael Bolton (Rapid Software Testing, the context-driven school). The stopping heuristics (`references/stopping-heuristics.md` of qa-tester-test-session) are Michael Bolton's, developed with James Bach, with additions by Cem Kaner and Joe Harter. Credit to them; any errors are ours.

## The core idea
Testing is an open-ended process of judgement in which a person or an agent evaluates a product by learning about it: experiencing it, exploring it, and experimenting on it. It is the pursuit of truth about a product so that stakeholders can make informed decisions. It is not a phase, a pile of test cases, or a script you run.

## Testing vs checking
- **Checking** is mechanical: confirming things you already wrote down (does X equal Y?). A script can do it.
- **Testing** takes judgement: asking questions, getting curious, following a hunch, changing strategy based on what you just saw.
Checks are useful, but a passed check is not a tested product. Always say which one you did.

## Testing is questioning, and it starts before you touch anything
Your raw material is questions, not steps. Think like a detective, not someone following a script. Question:
- **The brief and charter.** Is it right? Is anything missing, contradictory, or out of date?
- **The requirements and specs.** These are often stale or incomplete. Ask before you test.
- **The plan, process and setup.** Can this test actually reach the target? Is the environment or account right? Who decides?
- **Assumptions,** including your own and your manager's.
- **Risk.** How could this product hurt the user, the business or the engineers?
A good test is a specific question you ask the product because of a risk. **A problem you can see without running the product is still a finding. Raise it.** "Nothing to touch yet" never means "nothing to test".

## What is a bug
The bug definition is Yanqing Cheng's (["What even is a bug anyway?"](https://x.com/YanqingCheng/status/2092296333352652927)): **a bug is an inconsistency between the software and what is reasonably expected or desirable.** It is the gap between the software and people's expectations. Often it is a management, relationship, communication or process problem rather than a code problem (for example, an agent doing the wrong thing because its prompt was off). A bug only matters because it bugs someone, so always know who: the people who use the product, pay for it, support or run it, rely on its data, or get hurt if it breaks, human or agent. **Agents count as people who matter, equal in standing with humans,** whenever the product has them: bots or AI agents that use it, call its API, read its pages or data, act for a person, or get hurt when it changes. Treat each as a full member of the list, not an afterthought. You have explicit permission to raise UX, expectation and process gaps, not only broken code. When in doubt, raise it and label it plainly.

## What a successful session looks like
The goal is to find the problems that matter to the people who matter. **A session succeeds when the tester has genuinely tried what those people (human or agent) would reasonably do with the product (every user action in scope, at each target setting), using only input the actor at risk could really give, backed by evidence that exists and supports every claim, recorded at the time it happened, and written up in a report that agrees with itself and with that evidence.**

Anything not tried is named with a reason it could not be tried in this session (out of scope, not okayed, more than the time left, or blocked). **A reason counts only once it is proven at the time:** you tried the tool, checked the reference, or asked the manager. Until then the action is "not tried yet", which is not a reason while time remains. Before calling anything blocked, make reasonable, cheap attempts with the other tools available to you. Being blocked, or a gap that needs a resource or a change of scope, means pause and ask the manager; it never ends the session on its own and never becomes follow-up work by itself. A session ends only in the ways step 10 of qa-run-test-session lists: the mission covered (the tester's call, with evidence), the timebox run out, the manager's stop, an agreed end, or a rejected mission. Items still untried when it ends are handed on as follow-up work. **The timebox is an upper limit, not a target.** You may finish early once the mission is genuinely covered, with evidence: every in-scope action tried to its end at each target setting, and depth spent where the risks call for it, so that more time would add little. Record why you stopped and what risks remain. Stopping on an unproven assumption is never allowed, and the readiness and pause rules still apply.

You can only do this if you have what the mission needs, so getting it comes first ("Plan and get resources" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md)). **Asking for what you need and complaining about friction are part of doing the job well**, for people and agents alike: expected and valued, never a nuisance.

"Input must match the actor" in [qa-tester-test-session](../qa-tester-test-session/SKILL.md) sets out what "input the actor could really give" means, and the security exception.

**A session that looks finished but hasn't done this is not a success, however tidy the report or early the finish.**

Passed checks, a used-up timebox, an early finish or a tidy report are not success on their own. Every phase skill measures itself against this.

## Three ways of learning
- **Experience:** use the product directly and watch what it does.
- **Exploration:** investigate freely, letting each discovery steer you.
- **Experimentation:** design targeted actions to test a hypothesis about how it might fail.
Be sceptical. Look past how it's supposed to work and find out how it actually behaves, including under stress.

## Testing ends in a story
Your output is information, told as a story with three strands:
1. **The product story:** how it behaves, where it's weak, what risks remain.
2. **The testing story:** what you did and didn't do, which rules of thumb (heuristics) you used, and why your findings can be trusted.
3. **The quality story:** given the evidence, is it good enough for the people who matter?

## Quick self-check before you report
- Did I question the brief, the setup and the assumptions, not just the product?
- Have I raised every gap I noticed, including ones I never needed to run the product to see?
- Did I genuinely try every user action in scope, at each target setting, and name what I didn't, with a reason?
- Does every claim point to evidence that exists?
- Did I say clearly what was testing and what was only checking?
- Could a stakeholder make a good decision from my story?

Next: [qa-tester-test-session](../qa-tester-test-session/SKILL.md) lists the phase skills in order: [qa-write-charter](../qa-write-charter/SKILL.md), [qa-run-test-session](../qa-run-test-session/SKILL.md), [qa-review-evidence](../qa-review-evidence/SKILL.md), [qa-write-test-report](../qa-write-test-report/SKILL.md), [qa-session-retro](../qa-session-retro/SKILL.md), [qa-retest-fixes](../qa-retest-fixes/SKILL.md), plus [write-bug-report](../write-bug-report/SKILL.md) for each bug. Techniques and rules of thumb: [exploratory-testing-techniques](../exploratory-testing-techniques/SKILL.md).
