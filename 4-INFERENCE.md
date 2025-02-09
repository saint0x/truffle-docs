---
title: 'T.R.U.F.F.L.E'
description: 'Truffle's blazingly fast inference architecture, coming soon to Orb'
---

# T.R.U.F.F.L.E

*Truffle's Rather Unfortunately Fucking Fast LLM Engine*

At its core, the Truffle engine is an exercise in pushing the boundaries of inference performance. Our engine currently powers cloud-based inference with exceptional speed, and is designed to transition seamlessly to the Orb locally.

## The Philosophy

The challenge with modern LLMs isn't just running them - it's running them efficiently. Traditional approaches often sacrifice performance for flexibility or vice versa. We took a different path: what if we optimized specifically for inference, and nothing else?

This led to some interesting technical decisions:

### Memory First, Questions Later

Memory management in LLMs is typically a major bottleneck. Most solutions either:
- Waste memory for simplicity
- Sacrifice speed for memory efficiency
- Accept the limitations of their hardware

We approached this differently. 
Every component in our pipeline is optimized for speed:

- Custom attention implementation that pushes hardware limits
- Zero-copy token streaming for minimal overhead
- Dynamic batching that adapts to real-world conditions

The result? Response times that feel impossibly fast.

### Architecture That Scales

What makes Truffle special isn't just its speed - it's how it achieves that speed. Our architecture is built on three core principles:

1. **Intelligent Memory Management**
   The difference between good and great often comes down to cache efficiency. Our prefix cache system and page-based memory management allows us to be not just fast, but consistently fast.

2. **Hardware Awareness**
   Whether running in our cloud infrastructure or on your Orb, the engine understands its environment and adapts accordingly. This approach pushes hardware output to its limits, safely.

3. **Optimized Attention**
   We've reimagined how attention computation works in inference scenarios. The results speak for themselves - though we'll let our speed tests do the talking.



<Note>
Truffle's inference engine is currently powering our MacOS client.
You can try it out for free HERE.
</Note>
