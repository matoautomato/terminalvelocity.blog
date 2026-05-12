---
title: Agentic commerce and BNPL
subtitle: How does BNPL - which is human-in-the-loop to the core - become agentic?
date: 2026-05-12
description: How does agentic commerce fit into BNPL
tags:
  - "#payment"
  - "#fintech"
  - ai
  - "#opinion"
---

Everyone and their mother keeps talking about agentic commerce it would seem. That is, if you live in payment la la land. I can confidently say that none of my friends outside of this industry bubble have ever heard of such a thing, nor do they even remotely care. When I told my wife what my next blog post topic was, she was just shaking her head silently. Very understandably so, if I may add. 

Yet, the hype machine keeps going and agentic commerce is undoubtedly the dominant narrative in payments and e-commerce, at least since late 2025, and ever increasingly in 2026. So dominant, if not more so, than mobile commerce was a few years back. For the purpose of this blog post, we define agentic commerce as "single or multiple AI-agents executing end-2-end purchases on behalf of humans". 

If you need a TL; DR for the next 2500 words: agentic autonomy in e-commerce is still more a promise and - for BNPL - an infrastructure problem and a regulatory question that needs solving first. 

Now let's dive in, and immediately skip all the analyst forecasts. They range from [$5 trillion](https://fidoalliance.org/fido-alliance-to-develop-standards-for-trusted-ai-agent-interactions/) (with a t) commerce mediated by agents and [25% of global e-commerce](https://www.deloitte.com/us/en/Industries/consumer/articles/agentic-commerce-ai-shopping-agents-guide.html) enabled by agents by 2030 all the way to ChatGPT accounting for [less than 0,2%](https://pubsonline.informs.org/doi/10.1287/mksc.2025.0489) of all e-commerce sessions in 2025, with only [10% of all consumers](https://www.bain.com/insights/agentic-ai-commerce-hinges-on-consumer-trust/) buying anything through AI and [Gartner](https://www.metarouter.io/post/agentic-commerce-in-2025-what-we-learned) flat out saying that by end of 2027 over 40% of all agentic AI projects will be cancelled. Between all these extremes lies the failed OpenAI instant checkout project that was [scrapped after just 3 months](https://www.modernretail.co/technology/what-went-wrong-with-chatgpts-instant-checkout/) in March 2026. Take that how you will.

So instead of living in some vague future of overoptimism or bubble-bursting defeat, let's look at the two aspects of agentic commerce that are actually relevant, and by relevant I mean: for BNPL (as I keep getting asked about it): **Infrastructure** and **Regulation**.

## The infrastructure race currently unfolding

To say we are at the early stages would be an understatement. To say the infrastructure play is fragmented even more so. Note that when I talk about infrastructure, I narrow it down to the payment side of things. Here we have to observe things roughly in 3 layers: 

* Identity: Who the hell is this bot? Who authorised it / is it even authorised?
* Protocol: How does an agent actually communicate with a merchant?
* Product: What the merchant actually integrates to enable agentic commerce. 

### Identity: Who the hell is this bot?

Before any transaction can happen, a merchant (and frankly also any BNPL-provider) needs answers to three questions: Is this agent what it claims to be? Was it authorised by a real human? What is it allowed to do? As of today, multiple competing frameworks are trying to answer these. We haven't got a winner yet.

Visa built the [Trusted Agent Protocol](https://stripe.com/blog/introducing-our-agentic-commerce-solutions) (TAP) with Cloudflare – cryptographic HTTP signatures that let merchants verify an agent at the CDN layer without writing new code. Mastercard went a different route with [Verifiable Intent](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) – SD-JWT delegation chains that link identity, intent, and action into a cryptographic audit trail, co-developed with Google. Both are being contributed to the [FIDO Alliance](https://fidoalliance.org/fido-alliance-to-develop-standards-for-trusted-ai-agent-interactions/), which formed an Agentic Authentication Working Group in April 2026. No specs published yet.

On the startup side, [Skyfire](https://www.skyfire.xyz/) gives each agent its own digital wallet with USDC settlement, and [Experian](https://www.experian.com/blogs/insights/agent-trust/) launched an Agent Trust framework in April 2026 that binds a human identity to an agent via tokens and a registry.

The common theme: everybody agrees agent identity needs solving (urgently!), nobody agrees on how, and the players developing standards (like the FIDO Alliance) are at least a year away from publishing anything usable. The industry has at least coined the (very marketable) term – KYA, Know Your Agent – as the agent equivalent of KYC. But a catchy acronym is not a standard, and regulators haven't acknowledged the concept yet. Hype looks a bit different, if you ask me. 

### Protocol: How does an agent talk to a merchant?

Five competing open protocols are shipping simultaneously, some of them already bring their own identity layer, some only the protocol of interacting with the merchant:

| Protocol | Who's behind it | What it does | Focus |
|---|---|---|---|
| [ACP](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) (Agentic Commerce Protocol) | OpenAI + Stripe | Defines how an AI agent talks to a merchant backend to create and complete a checkout session. Three API calls: create cart, confirm, complete. Open source, Apache 2.0. | Checkout only |
| [UCP](https://developers.google.com/merchant/ucp) (Universal Commerce Protocol) | Google + 20 partners (incl. Shopify, Walmart, Stripe, Visa, Mastercard) | Broader than ACP – covers the full journey from product discovery through checkout and payment. Built on REST/JSON-RPC, integrates multiple sub-protocols (AP2, A2A, MCP). Also Apache 2.0. | Full commerce journey |
| [AP2](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) (Agent Payments Protocol) | Google + 60 contributors (Mastercard, PayPal, Coinbase) | The identity and payment layer within UCP. Uses verifiable digital credentials to prove who the agent is, who authorised it, and what it's allowed to spend. Donated to the [FIDO Alliance](https://fidoalliance.org/fido-alliance-to-develop-standards-for-trusted-ai-agent-interactions/) for standardisation. | Identity + payments |
| [MPP](https://stripe.com/blog/machine-payments-protocol) (Machine Payments Protocol) | Stripe + Tempo | Built for machine-to-machine payments – micropayments, streaming payments, recurring agent transactions. Works in both stablecoin and fiat. Cloudflare integrated. | Micropayments |
| [x402](https://www.x402.org/) | Coinbase | Repurposes the HTTP 402 "Payment Required" status code for native stablecoin payments. Stateless, no session overhead, zero protocol fees. 119M transactions on Base alone as of March 2026. | HTTP-native crypto payments |

If you're reading that table and thinking "oh my god, this looks like five competing standards that partially overlap, built by companies that are partnering and / or competing with each other" ...well, congratulations, that's 100% accurate. Stripe co-authored ACP with OpenAI while also endorsing Google's UCP. Google leads UCP but also leads AP2, which sits inside UCP but is its own open-source project donated to FIDO. Confused yet? 

Coinbase's x402 doesn't care about any of them and just does its own HTTP-native thing, while [laying off 14% of staff](https://techcrunch.com/2026/05/05/coinbase-to-lay-off-14-of-staff-as-part-of-broader-restructuring/) and having non-techies [vibe-code new products](https://www.pymnts.com/artificial-intelligence-2/2026/vibe-coding-breaks-into-banking-before-regulators-can-react/) and [suffering a multi-hour outage](https://www.coindesk.com/business/2026/05/08/coinbase-disruption-tied-to-aws-outage-draws-criticism-amid-staff-layoffs-and-q1-losses). I rest my case.

### Product: What you actually integrate

This is where it gets interesting. Protocols are specs on paper – products are what merchants and payment providers actually plug into.

**[Stripe](https://stripe.com/blog/introducing-our-agentic-commerce-solutions)** is everywhere. They co-authored two protocols (ACP, MPP), endorse a third (UCP), and ship the products that implement all of them. Their key solution is [Shared Payment Tokens](https://docs.stripe.com/agentic-commerce/concepts/shared-payment-tokens) (SPTs) – scoped grants that let an agent use a buyer's payment method, bounded by time, amount, and seller. SPTs now support card-on-file, network tokens (Mastercard Agent Pay, Visa Intelligent Commerce), and BNPL (Klarna, Affirm). Stripe claims to be the only provider unifying all three through a single primitive. They also very recently shipped [Link Wallet for Agents](https://stripe.com/blog/giving-agents-the-ability-to-pay) – programmatic access to their digital wallet. At Stripe Sessions 2026 they announced 288 new products, the majority AI-related. If AI has a "hype-man" in payments, it's Stripe, let's face it.

**[Adyen](https://www.adyen.com/)** takes a merchant-first approach. Their Universal Token Vault is processor-agnostic and bank-grade. They're working with Google, OpenAI, Visa, and Mastercard – but the focus is on merchants controlling their own checkout, not ceding it to an agent platform. Still in beta, still very early days.

**[Shopify](https://shopify.dev/docs/agents)** has the most advanced platform integration. Their Catalog API exposes products to agents via REST and MCP, natively supporting both ACP (ChatGPT) and UCP (Google AI Mode). Checkout Kit lets agents complete purchases. They're the closest thing to a merchant-side standard.

And then there is **[PayPal](https://newsroom.paypal-corp.com/2026-01-08-PayPal-Powers-Microsofts-Launch-of-Copilot-Checkout)** in the Microsoft Copilot Checkout alongside **[Stripe](https://stripe.com/newsroom/news/microsoft-copilot-and-stripe)**. That's it about PayPal.

### So what does this mean for BNPL?

So the three infrastructure layers solve for general problems, some of those also touching BNPL, especially the identity bit. Identity is one of the *key factors* for fraud risk management in BNPL, and for over a decade, every checkout and payment provider on this planet has optimised for humans and blocked every bot interaction when spotted. That definitely requires a pivot, which is only possible if the identity piece is solved safely, by whichever winners emerge in the infrastructure race. 

But, none of these three layers solve the actual hard problem for BNPL: how does an agent trigger a credit decision, capture legally valid consumer consent to BNPL terms, and authenticate the consumer – all without a human in the loop? The identity layer can verify the agent, the protocol layer can route the checkout, and the product layer can process the payment. But the bit in between – "does this human actually want to take on credit right now, and have they agreed to the terms?" – has no clean answer.

The closest thing is maybe Stripe's SPT, which now supports Klarna and Affirm alongside card tokens. But SPT is a Stripe standard, not an open standard. If you're a BNPL provider not on Stripe, you currently have no equivalent. Your options are: integrate with Stripe, build direct network-level integrations with Mastercard Agent Pay or Visa Intelligent Commerce, or wait for FIDO standards to mature (2027–2028 at the earliest). None of these options are really optimal. Maybe you should just – dare I say it – wait. [Forrester concluded](https://www.forrester.com/blogs/what-it-means-that-the-leader-in-agentic-commerce-just-pulled-back/) that agentic commerce "suffers from having been overhyped too early." So waiting to see which standard actually brings solutions, might be viable. 

The root cause for this "human-in-the-loop" conundrum is rooted in the regulatory requirements. If you are still reading this, let's dive into it. 

## The Regulatory race that doesn't deserve the name

Now, if you're thinking "oh boy, the infrastructure bit was confusing as hell and slow and fractured" – welcome to the regulatory hell, where current frameworks don't even know what AI agents are.

{{< figure src="thisisfine.webp" alt="This is fine meme" caption="Move on, nothing to see here." >}}

A card-on-file agent transaction is relatively straightforward: the agent presents a scoped token, the card network processes it. No credit decision, no consent to new terms. BNPL is fundamentally different – every transaction involves a credit decision, legally mandated disclosure, and explicit consumer consent. And that's where regulation has something to say. No, I'm sorry. That's where regulation has *a lot* to say. 

### The human-in-the-loop requirement

Both the EU and the UK are tightening BNPL regulation in 2026, and – in a nice bit of irony for post-Brexit Britain – they landed on essentially the same rules independently. Take that, Reform UK.

The EU's [CCD2](https://eur-lex.europa.eu/EN/legal-content/summary/consumer-credit-agreements-2023.html) (Consumer Credit Directive, adopted 2023, rules apply November 2026) mandates adequate creditworthiness assessment before *each* credit decision, explicit disclosure of terms, and clear consumer consent. The UK's [FCA BNPL regulation](https://www.cbschangepartners.co.uk/blog/fca-targets-bnpl-major-regulatory-shift-in-2026) (oversight begins July 2026) extends the same creditworthiness requirements to low-value and interest-free BNPL – which was [previously unregulated](https://www.concentrix.com/en-gb/insights/blog/bnpl-regulation-uk-2026-lenders-retailers/). Neither framework mentions AI agents. Neither needs to – the requirements are clear enough: *a human must consent to credit terms before credit is extended*.

Ask yourself if your bank would grant you a mortgage if you sent your chatbot to negotiate with them. It's not the exact same thing, but in spirit and much of the legal framework – it is.

The technology to merge an agentic checkout with a human-in-the-loop approach exists. Any agentic workflow could be paused to wait for a consumer to consent to the BNPL terms presented in a 2FA or authentication step. The agent receives the green light from the consumer and continues doing its thing. Whether regulators would be happy with that remains to be seen. 

### The liability vacuum

And then there's the question nobody wants to answer: when an agent screws up a BNPL transaction, who pays? What keeps getting lost in this whole debate is that we are *dealing with non-deterministic tools to create predicted behaviour* - "buy me exactly what I want for the best price and the conditions I accept." Try prompting this into three different AI models and see what happens. Any product manager who has ever run an AI eval will tell you how reliable LLM output is. 

The EU's [AI Liability Directive was withdrawn](https://www.insideprivacy.com/european-union-2/the-eu-considers-changing-the-eu-ai-liability-directive-into-a-software-liability-regulation/) in February 2025 – member states couldn't agree. This removed the expected civil liability framework for AI-caused harms. If an agent erroneously initiates a BNPL agreement on a consumer's behalf, liability between consumer, agent platform, and BNPL lender is *legally undefined*. Who pays for the damages?

[PSD3](https://www.nortonrosefulbright.com/en/knowledge/publications/cedd39c6/psd3-and-psr-from-provisional-agreement-to-2026-readiness) doesn't help either – political agreement reached November 2025, full compliance not expected until [late 2027 or early 2028](https://www.dlapiper.com/en/insights/publications/2026/03/psd3-and-psr), and it does not explicitly address AI agents as payment initiators. Europe is in an [implementation gap](https://www.reply.com/en/strategy-and-business-model-transformation/agentic-checkout-beyond-the-hype), and nobody is in a rush to close it.

So until regulatory frameworks – which tend to be rather localised – create clarity in handling agents for BNPL and credit-adjacent payment products, the human-in-the-loop approach is the absolute minimum. And even if the infrastructure race produces one or two global standards for identity and protocol, until local regulation catches up, adoption will drag.


## Bubble Now, Bust Later

So, all in all, we can confidently say, when it comes to agentic commerce in general and specifically for BNPL payments: we are in the early days. At the current speed of things that might not mean much more waiting, at least not for the technical side of things, but it will definitely mean waiting on regulators to wake up to what the industry has cooked again. 

And those are just the entry gateways for BNPL to participate in the alleged agentic revolution. Looking inwards there is definitely more homework to be done. Fraud models need to change fundamentally. Today they assume one human, one checkout. In an agentic world it's one human, N agents, all taking on debt independently. See why that identity layer matters?

Not to mention that opening up to synthetic IDs comes definitely at a bad time, where agents have allowed fraudsters to commit synthetic identity fraud at an unprecedented scale – it was the fastest growing fraud type globally with an [8x YoY increase](https://risk.lexisnexis.com/global/en/about-us/press-room/press-release/20260326-ccr-global-fraud).

So maybe – just maybe – you should follow the example of my wife, shake your head silently, have a cup of tea and watch this race unfold, to see the clear winners in these big infrastructure bets. Maybe take all that newfound time to browse through all the virtual storefronts that have been lovingly crafted for your human eyes, buy yourself something nice, and pay later. 