---
title: The myth of collapsing build costs
subtitle: Who actually pays for the AI-driven 10x?
date: 2026-06-11
description: A receipts-driven takedown of the "AI is collapsing the cost of building software" narrative, via Adam Bender's Google I/O 2026 keynote.
tags: [ai, opinion]
---

Whatever your stance on AI is, you are either observing with a bag of popcorn or feeling with your wallet the true costs of handing over your work to an LLM.

It's been my personal meme to basically mention in every blog post about AI in the past 6 months that the compute bill is being footed by some desperate VCs who are betting (hoping) for the next 10–100x opportunity. You, your team, your company hasn't even paid a fraction of the true cost with your Claude subscription. Yet. That all changed in the past weeks, to apparently everyone's great surprise.

So here it is, my personal rundown of the true cost of compute.


## I brought the receipts

Let's do a quick round of numbers and receipts, so the rest of this blog post isn't just me vibing about the collapse in AI demand due to CFOs panicking about non-deterministic costs.

- **Anthropic [announced on June 2](https://www.techtimes.com/articles/317625/20260602/anthropic-ends-subscription-subsidy-agents-june-15-credit-pool-replaces-flat-rate-access.htm) that, starting June 15, 2026, Claude Agent SDK and automated workloads will be carved out of the existing subscription pool** and pushed onto [a separate monthly credit](https://www.pravinkumar.co/blog/claude-june-15-billing-change-explained-2026) – $20 for Pro, $100 for Max 5x, $200 for Max 20x – billed at standard API list rates once exhausted. Interactive chat keeps its flat-rate ride. Translation: people going mad with 24h agentic loops ate their compute.
- **GitHub [paused new Copilot Pro / Pro+ / Student signups on April 20, 2026](https://thenextweb.com/news/github-copilot-signup-pause-agentic-ai-usage-limits).** [Their VP of product said the quiet part out loud](https://www.infoworld.com/article/4161278/github-pauses-new-copilot-sign-ups-as-agentic-ai-strains-infrastructure.html): agentic workflows "are routinely consuming more compute than users pay for in a month." Copilot Free is now the only plan accepting new individual sign-ups. Flat-rate math doesn't add up. Who would've thought.
- **[Uber burned through its entire 2026 AI budget by mid-April](https://fortune.com/2026/05/26/uber-coo-ai-spending-tokens-claude-code/)** (Fortune, May 26 2026). Per-engineer Claude Code costs landed at **$500–$2,000/month**, blowing past internal forecasts. The COO is on the record saying he can't link the spend to better consumer features: *"That link is not there yet."* I mean, it's on brand for a company whose entire DNA is "let's set money on fire until a market exists."
- **Microsoft's own [leaked internal reports](https://fortune.com/2026/05/22/microsoft-ai-cost-problem-tokens-agents/)** (Fortune, May 22 2026) conceded that for several agentic workloads the token bill exceeds the cost of the human employee the agent was supposed to augment.
- **[Stanford's Digital Economy Lab](https://digitaleconomy.stanford.edu/publication/how-do-ai-agents-spend-your-money-analyzing-and-predicting-token-consumption-in-agentic-coding-tasks/)** measured that agentic coding tasks consume roughly **1,000x more tokens** than chat-style reasoning, with input tokens (not output) driving the cost – every step re-reads the entire prior context, building a "pricey context snowball." Same task, same model: token usage varies up to **30x run to run**, and higher token spend does not correlate with higher accuracy.
- **[Gartner pegs the enterprise AI coding agent market at $9.8–11.0B annualised](https://www.gartner.com/en/articles/enterprise-ai-coding-agent-market)** as of April 2026, with vendors mid-pivot from seat-based to usage-based pricing across the board.

Subscription pricing was a loss-leader – even before agentic loops killed the chatbot and led to the explosion in compute costs. All of this is being walked back as I write this, and the actual economics are landing on engineering budgets right now.


## But tokens are just half the story

The token spend is currently showing up on your bill if you are racing to be an early adopter of AI in every single (software development) process, maybe because you or your leadership has FOMO and / or are comprised of [Business Idiots](https://www.wheresyoured.at/the-revenge-of-the-business-idiot/).

Recently a teammate shared [this talk from the recent Google I/O](https://www.youtube.com/watch?v=9t9Kj2f6wtU), delivered by Adam Bender, where he explores the absolutely inevitable impact AI is undoubtedly going to have on every single tech team on this planet. Do I need to point out my sarcasm? I hope not.

It's a stark reminder of the implicit costs of AI adoption, contrary to the explicit one showing up on your Anthropic bill. And the economist in me could not skip it – I had to listen to the whole thing front to back.

The first 20 minutes of the talk are spent on some elaborate preface on systems thinking, interconnectedness, your entire department finding itself and realising that they are all *one software development ecosystem*. Never knew systems thinking could sound like a Bali yoga retreat, but here we are.

Let's be frank: this is a Google keynote, and *every single speaker on that keynote* is a salesman for Google and its products. Don't let an elaborate and esoteric intro distract you from that. Because once that 20-minute intro finishes, comes the actual point of the entire talk, that allows for no pushback, no pullback and no counterpoint.

I quote:

> "Every developer ecosystem around is going to have to wrestle with this 10X. It's coming."

No evidence, no mechanism, no "here is what would have to be true for this not to happen." It's coming. Full stop. Buckle up, nerds! You will 10x with AI, and with that your entire developer ecosystem will fold into a huge transformation. All your established systems will break.

And within that transformation and ecosystem destruction lie – and this is my point – enormous costs, that put the entire AI adoption narrative in an even worse light. The true cost of tokens is just the tip of the iceberg.


## OK, then let's go through it point by point

For each of Bender's "transformations": what he claims will break, what it actually costs, and – most crucially – who collects the cheque.

1. **Source code explosion.** He talks about 10x more code *while quoting Atwood with "Software is a liability"*. The irony is not lost on me. So you have 10x more liability, plus a retraining bill nobody budgeted for. [Veracode](https://www.veracode.com/resources/analyst-reports/2025-genai-code-security-report/) says AI-generated code carries 2.74x more vulnerabilities, [CodeRabbit](https://www.coderabbit.ai/blog/state-of-ai-vs-human-code-generation-report) clocks 1.7x more issues in AI-coauthored PRs. But whose products could help you with all that load? *Anthropic, OpenAI, Cursor, GitHub, and yeah,* **Google.**
2. **Builds get bigger and more frequent.** Agents trigger more compiles, not just bigger ones. Google itself is "bumping into" (lol!) binary-size limits. So who are all those cloud providers who could help you with those pesky limits? Ah yeah: *GCP Cloud Build, AWS CodeBuild, Azure Pipelines, and yes* **Google**!
3. **Microservices chatter 10x.** You want to create 10x code, in 10x microservices, which means 10x network calls bouncing around? Enjoy, your egress fees and your service mesh sidecars chewing CPU and memory. Also, someone will have to trace and log all of those calls, won't they? Who collects on this? *AWS, Azure, and yes,* **Google** *on egress; Datadog, New Relic, Honeycomb on telemetry; Google Cloud Observability bundled into GCP if you're already in their ecosystem. So once again:* **Google.**
4. **Code review collapses.** Why? Because no human is capable of reviewing 10x code. Either humans slow everything down or you bolt on an AI reviewer onto the whole thing – tokens reviewing tokens that wrote tokens. Tokens! And who could do that for you? *CodeRabbit, GitHub, Cursor, Claude Code, and yes, you guessed it:* **Google** *via Gemini Code Assist.*
5. **Token sprawl.** "Do you know where the tokens are going right now?" Spoiler: no, and now you need FinOps tooling to find out (they probably disappeared in your AI code review, but don't let that stop you). And yes, please pay for services or tokens by: *Anthropic, OpenAI,* **Google** *(again!?), plus a whole new industry of AI FinOps startups.*
6. **Test infra 100–1,000x.** The one place where Bender drops the systems-thinking dressing and just says it: *"this is a line item in your budget at some point."* Because that bill will be *crazy*. Agents love running tests because tests tell them they're actually producing something that works. If AI also *writes* the tests, you pay for inference and CI. You could pay **Google** for it, even *twice*, for GCP + Gemini.
7. **Version control bottlenecks.** Git wasn't built for 10x commit velocity, and lots-of-tiny-repos isn't a fix (Bender himself: *"an entirely different set of challenges, none of which AI will make easier"*). So you end up paying for managed monorepo hosting *or* sinking a multi-quarter migration project into Bazel – which **Google** open-sourced from their internal Blaze and which conveniently nobody understands as well as ex-Googlers do. Hosting cheque: *GitHub Enterprise (Microsoft), GitLab Ultimate*.
8. **Rollback safety inverts.** Today, rollbacks work because you release software *slightly slower* than you can detect a problem in production. AI-driven release cadence breaks that and then every rollback contends with the next ten releases stacked on top of it. So who could sell you continuous deployment tooling, feature flags, and the observability you'll need to find the problem before it gets buried in the next releases? The usual suspects, like Argo CD, Harness, LaunchDarkly, Datadog, and yes, **Google** *again, via Cloud Deploy.*
9. **All your internal APIs are now public.** Bender's quote: *"Agents aren't going to negotiate with you. If they can get access to your data, they will do it."* How reassuring! Now every internal endpoint you've ever shipped needs internet-grade hardening, because the agent doesn't care that you marked it `internal-only` in a Confluence page. Enjoy your multi-quarter security engineering programme. Who could help you with that? *Kong, AWS API Gateway, Auth0, HashiCorp Vault, Snyk, Veracode, and – plot twist – Apigee, owned by* **Google.**
10. **Jevons' paradox on tokens.** Bender's own line: tokens *"will end up everywhere in your workflow"* and you'll be *"putting a cost on previously-hidden work that was invisible before."* Translation: every step in your dev process that used to be free now has a metered API attached to it. Cool. Bonus points: that metered API is rate-limited, externally hosted, and now sits on the critical path of the most basic engineering work. Who sends you the bill? *Anthropic, OpenAI, and* **Google**.
11. **Democratised tool sprawl.** Every engineer brings or demands their own AI stack. The "solution" your CTO will land on: standardise on one stack – aka: lock-in to single-vendor exposure, eating whatever shit sandwich pricing is put in front of you. Who is selling exactly that one-stack answer right now, with Gemini Code Assist + Vertex + GCP wrapped in a bow? Ah, yes: **Google.**
12. **Juniors with 50 agents and no judgment.** Bender's actual question: *"How do I teach ten years of experience in six months?"* He doesn't know, because you can't. This one is pure cost transferred straight onto your engineering team in the form of slower onboarding, senior-engineer babysitting, more incidents, more attrition. The vendors *do* still get paid for the 50 agents the junior is hammering, of course.
13. **Human attention as the new scarce resource.** Bender says that *"Human attention is the most precious resource we have."* and that historically we were saved by the fact that *"we couldn't make more trouble for ourselves than we could make attention to."* In all of that insane (newly created) agentic noise the human is supposed to retain context and make informed decisions. Who gets paid for this? Nobody, directly – it's just cognitive load. But the noise eating your team's attention – the slowdowns, the fatigue, the burnout – is generated by agents that someone in your org is paying *Anthropic, OpenAI, or* **Google** *for.*

So, to absolutely no one's surprise, across all 13 points, the real beneficiaries of that cost explosion are: **Anthropic, OpenAI, GitHub/Microsoft, the hyperscalers,** and **Google in basically all 13.** Almost every single "inevitable transformation" Bender names maps to at least one product Google sells.

And the pitch is the sheer inevitability of it all, which is never questioned, even once.

It is truly ironic that a keynote supposed to showcase the foresight and wisdom of Google engineering "in the age of AI" is basically an anti-ad for any concept-less, "all-in" AI adoption devoid of factual use cases, if you look at it critically for more than 10 seconds.

The path to profitability for all those hyperscalers and AI-companies is one side of the coin, the ROI of adopting AI-services from them is a completely different one. How the ROI of AI still remains a myth was [described very eloquently by Ed Zitron in a recent blog post](https://www.wheresyoured.at/ai-doesnt-have-roi/). My analysis of this Google I/O keynote shows that really the real cost on one's bottom line goes much, much deeper, if we all collectively believe in a world ruled by clankers.

{{< figure src="ai_tape.jpg" alt="Companies fixing leaking costs caused by AI with the universal tape AI" caption="Gotta fight fire with fire, right?" >}}

## Let me be the prophet for five minutes

Given this shift in cost awareness that [even surprised Sam Altman](https://www.tomshardware.com/tech-industry/artificial-intelligence/openai-ceo-sam-altman-admits-ai-token-costs-are-becoming-a-huge-issue-company-seeks-improved-value-as-overspending-becomes-a-meme) (I jest), no one knows what the near future will bring, but I can take some wild guesses, and then come back to it in 12 months and shake my head when I get them all wrong.

* Hype-driven AI adoption will be replaced by cost and ROI focus. Once the CFOs take over again (and they always do, in cycles, if you have played this game long enough), things might actually slow down *a lot*.
* Token budgets per developer will be a thing, and will most likely be abused to control engineering like "lines of code produced" are being abused by imbeciles cosplaying as VP Engineering today.
* Despite all my sarcasm in this post, my unyielding belief in humanity drives me to hope that techies will finally try to find *actual use cases* where AI adoption might improve their processes at acceptable costs.
* Localised, on-premise AI infrastructure will become the norm for enterprise businesses (and probably even for SMBs). Open-Source models will catch up with frontier models, like they always do, within 12 months.
* All of the above will hurt the bottom lines of the big hyperscalers, soon-to-be public AI companies, and put big question marks on big tech's scale of AI investments.

With the manic speed of things unfolding, I think I can return to this post in just a few months, at the latest after the IPOs of the big names. I'll see you on the other side of the next earnings call, with my popcorn in hand.
