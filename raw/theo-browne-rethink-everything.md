---
source: https://youtu.be/TV6f2weVgCI?si=PeU6ArrLtz8w7p1b
title: "It's Time To Rethink Everything"
author: Theo Browne
date: 2026-07-08
tool: summarize
---

# It's Time To Rethink Everything by Theo Browne

Theo Browne argues that AI has fundamentally broken the assumptions software engineers have relied on for decades, and that builders should be far more ambitious than they currently are. He draws a parallel to the cloud computing shift: before AWS, teams had to pre-provision servers and predict demand, making experimentation expensive and risky. The cloud removed that constraint, letting products start small and scale dynamically without massive infrastructure teams. He argues AI is doing the same thing again, but this time to entire engineering teams rather than just servers—Amazon-tier scale is now achievable without Amazon-tier hiring or capital risk.

Browne walks through several "obvious" limitations he no longer believes are fixed: why .env files can't be committed to a shared repo, why files can't live in two folders at once, why compilers require a real filesystem and kernel, and why codebases and dependencies still matter when an agent can rewrite an entire project's language and architecture in a week. *"The code base itself is useful as a resource for the agents, but the code itself doesn't really matter the way it used to."* His broader point is that companies like Salesforce won by covering both the full breadth of features companies need and unlimited depth in niche use cases—something small teams could never match before, since 95% of customers only need 5% of features, but that 5% varies wildly by customer. AI now lets small teams cover that same breadth, while depth can be left to the end user's own agent to fill in.

To prove the point, he demonstrates a project called Lakebed, a minimal cloud platform he built from scratch—including its own CLI, front-end and back-end frameworks, bundler, language runtime, and compiler—to collapse the gap between building an app (now minutes) and deploying it (traditionally hours, often stalled indefinitely). In a live demo, he deploys a working app with real sync and auth in seconds, then has an AI coding agent turn it into a live Kanban board with chat, deploying updates instantly. He's explicit that Lakebed isn't meant for production-scale products like Facebook, but as a proof that these fundamentals can be rebuilt. He closes by urging developers to attempt projects that feel oversized or "stupid," since the old constraints that made big rebuilds impractical no longer apply: *"You're not building big enough, and I'm saying that because I still don't think I am."*
