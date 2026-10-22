---
name: what-is-testing
description: >-
  Read first, before any QA charter or test session, and whenever you're unsure
  whether something counts as a test finding or is worth raising. High-level
  explainer, in plain words, of what testing is and what a bug is.
---

*Version: 2026-10-22.r17 (r17: context-driven review fixes (r17c draft: decisions under stated uncertainty, proportionate review, report and retro content required with flexible shape; r17b: reasoned stops told to the manager at once; success as useful information with sampling and gaps, risk-led breadth and depth, colours information only, adaptable report and variants; confirm and retro always done); skill names without the 'qa' prefix; no separate skill for checking fixes: a change is chartered like any other request ("Chartering a change" in write-charter); earlier: pre-publication fixes: endings match step 10; r16: timebox is an upper limit: finish early once the mission is covered with evidence; stopping-heuristics credit)*
# What is testing

The ideas come from James Bach and Michael Bolton (Rapid Software Testing, the context-driven school). The stopping heuristics (`references/stopping-heuristics.md` of test-session) are Michael Bolton's, developed with James Bach, with additions by Cem Kaner and Joe Harter. Credit to them; any errors are ours.

## The core idea
Testing is an open-ended process of judgement in which a person or an agent evaluates a product by learning about it: experiencing it, exploring it, and experimenting on it. It is the pursuit of truth about a product so that stakeholders can make informed decisions. It is not a phase, a pile of test cases, or a script you run. (Agent testers are this pack's adaptation of Bach and Bolton's human-centred description, not a claim they make: an agent tester takes the same responsibility for its judgement, says where its interpretation is uncertain, and asks for human review where the people who matter need it.)

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
The bug definition is Yanqing Cheng's (["What even is a bug anyway?"](https://x.com/YanqingCheng/status/2092296333352652927)): **a bug is an inconsistency between the software and what is reasonably expected or desirable.** It is the gap between the software and people's expectations. Often it is a management, relationship, communication or process problem rather than a code problem (for example, an agent doing the wrong thing because its prompt was off). A bug only matters because it bugs someone, so always know who: the people who use the product, pay for it, support or run it, rely on its data, or get hurt if it breaks, human or agent. **Agents count as people who matter, equal in standing with humans,** whenever the product has them: bots or AI agents that use it, call its API, read its pages or data, act for a person, or get hurt when it changes. Treat each as a full member of the list, not an afterthought. Equal standing doesn't mean identical testing: an agent user has its own expectations, its own means (requests, parsing, the pages or API the product offers it) and its own oracles (illustration: whether a page's structure and data can be read reliably, rather than whether it looks right), so test each kind of user, human or agent, through its own means and oracles. You have explicit permission to raise UX, expectation and process gaps, not only broken code. When in doubt, raise it and label it plainly.

## What a successful session looks like
The goal is to find the problems that matter to the people who matter. **A session succeeds when it gives the people who decide useful, credible information about the mission: what the tester learned about the risks that matter to the people who matter (human or agent), using only input the actor at risk could really give, backed by evidence that supports each claim, recorded at the time it happened, and written up in a report that agrees with itself and with that evidence, including how the tester sampled the product, what was left out and why, and how sure they are.** Trying every user action in scope at each target setting is not the measure of success: a list of user actions is a coverage aid the tester chooses and uses with judgement, and the report says what was sampled and what wasn't.

Anything in scope not tried is named with a reason: not selected because another investigation had more value (say which and why), out of scope, not okayed, out of time, or blocked. **Give each reason with the evidence you have and how sure you are**: you tried the tool, checked the reference or asked the manager, or you say plainly that it is unverified. Decisions under stated uncertainty are fine; hiding the uncertainty isn't. Before calling anything blocked, make reasonable attempts, in proportion to what unblocking it is worth, with the other tools available to you. **Stopping is the tester's reasoned decision** (step 10 of run-test-session): you may end the session on your own judgement, including when blocked, when a stopping heuristic fires or when no interesting questions remain, and you tell the manager straight away with the stopping reason, what was covered and the remaining risk. When a resource or a change of scope could unblock the mission, pausing to ask is preferred, but it isn't required. Items still untried when it ends are handed on as follow-up work. **The timebox is an upper limit, not a target.** You may finish early once the mission is genuinely covered, with evidence: the mission's questions answered as well as the evidence allows, the risks that matter explored in proportion to their importance, and the sampling and gaps stated, so that more time would add little. Record why you stopped and what risks remain. A stop needs its reason, with the evidence behind it and any uncertainty stated; a stop that hides an unverified assumption is the failure, not the uncertainty itself.

You can only do this if you have what the mission needs, so getting it comes first ("Plan and get resources" in [test-session](../test-session/SKILL.md)). **Asking for what you need and complaining about friction are part of doing the job well**, for people and agents alike: expected and valued, never a nuisance.

"Input must match the actor" in [test-session](../test-session/SKILL.md) sets out what "input the actor could really give" means, and the security exception.

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
3. **The quality story:** what the evidence suggests about the value and risks for the people who matter, so that the people who decide can judge whether it is good enough. The tester informs; the manager or PO decides.

## Quick self-check before you report
- Did I question the brief, the setup and the assumptions, not just the product?
- Have I raised every gap I noticed, including ones I never needed to run the product to see?
- Did I explore the risks that matter, and say how I sampled, what I left out and why?
- Does every claim point to evidence that exists?
- Did I say clearly what was testing and what was only checking?
- Could a stakeholder make a good decision from my story?

Next: [test-session](../test-session/SKILL.md) lists the phase skills in order: [write-charter](../write-charter/SKILL.md), [run-test-session](../run-test-session/SKILL.md), [review-evidence](../review-evidence/SKILL.md), [write-test-report](../write-test-report/SKILL.md), [session-retro](../session-retro/SKILL.md), plus [write-bug-report](../write-bug-report/SKILL.md) for each bug. Techniques and rules of thumb: [exploratory-testing-techniques](../exploratory-testing-techniques/SKILL.md).
