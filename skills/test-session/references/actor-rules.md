# Actor rules

Part of [test-session](../../test-session/SKILL.md). Open when you name a risk's actor or an oracle, when an action fails, when you write a finding, and in the evidence review. Every-phase rules: `test-session/references/session-rules.md`.

## Work through the product as its actors do

Test through the means the product's actors have (its interface, the requests and pages it offers an agent). Observe the runtime evidence the actor's environment shows (console, network, dev-server and build output) as you go. **Read code, repo data, diffs or server-side logs only when the charter names them as an oracle**, and agree first before reading anything holding other people's data. Report the symptom and its evidence, not a cause in the code. A cause the charter didn't ask for is a labelled hypothesis at most (step 4 of [write-bug-report](../../write-bug-report/SKILL.md)).

## Input must match the actor

Each risk has an actor: a person or agent who could cause the problem, or who meets it by using or viewing the product. **Use only input that actor could really give, through the means they really have. Every finding names its actor.**

- Ordinary users and agents: only their real means count: pointer, touch, keyboard, assistive technology, or for an agent the requests and pages the product offers it. A control is usable if their means reach it (a keyboard user may tab to a button under an overlay). Forced clicks, dispatched or injected events, editing the page or its storage, and calling code directly don't count. A result reached only that way is not a finding for them.
- Tool or product? When an action fails, report what you saw promptly, with how sure you are. Then pick isolation experiments by value and cost: another driver (headed instead of headless), another machine or account, a log or network trace, a minimal repro. Where useful, repeat the same means through another driver. Treat each experiment as evidence for competing causes, not proof by itself. Call it a tool limit only when evidence shows your tool caused it. A different means succeeding doesn't clear the failure: if the pointer fails but the keyboard works, the pointer failure stands, and the keyboard route is a workaround to report with it.
- Nobody needs to act for some findings (wrong content, metadata, contrast, broken layout, a leak). Their actor is anyone who views or fetches it.
- Security risks (a hostile actor who bypasses the interface): forced or forged input is the point. Probe that way only when the charter names the risk and actor, and only through the risky-probe gate. The finding must show the hostile actor has the access and steps it needs, and report only the impact you demonstrated.
- **Always report a security surprise** found by ordinary testing (a page load shows another account's data), with actor, evidence and confidence. The charter and gate limit investigation, never reporting. Ask before probing further. If the manager agrees, add a dated charter change and gate the probe.

*Illustration:* a script force-clicks a disabled "Launch" button and the page crashes. No visitor can press it, so it is not a finding for visitors. It matters only in a chartered, gated tampering session, reported as "someone who edits their copy of the page can crash it".

