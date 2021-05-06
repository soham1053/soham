+++
author = "Soham Patil"
categories = []
date = 2021-05-05T02:35:00Z
description = ""
draft = true
image = "/images/corso.jpg"
title = "Anthony Corso: SISL, AI Safety, and Julia"
type = "post"

+++
Anthony Corso is a post-doctorate researcher at the [Stanford Intelligent Systems Laboratory](http://sisl.stanford.edu/ "SISL"), a.k.a. SISL, pronounced "sizzle" :). He wrote his [PhD thesis](http://anthonylcorso.com/wp-content/uploads/2021/02/thesis.pdf "ALGORITHMS FOR BLACK-BOX SAFETY VALIDATION") about algorithms for black-box safety validation of autonomous vehicles, he's the executive director of the [Stanford Center for AI Safety](http://aisafety.stanford.edu/ "Stanford Center for AI Safety"), he wrote a deep reinforcement learning framework in Julia, and I recently got the chance to speak with him.

### Black-Box Safety Validation

Autonomous vehicles are being hyped more and more nowadays, but how can we ensure their safety? In this chunk of our conversation, we focused on [one part](https://arxiv.org/pdf/2004.06805.pdf "Interpretable Safety Validation for Autonomous Vehicles") of Anthony's thesis: finding relevant scenarios in which to test the vehicle. Anthony worked on a way to generate dangerous scenarios for these vehicles in simulations, so that their safety can be interpreted by humans without risk. Here, black-box means creating scenarios automatically, without the help of humans or manual labor. Firstly, most previous generators produced scenarios too complicated (high dimensional) for humans to interpret or chose scenarios irregardless of how unrealistic they are (imagine a jaguar jumping onto the vehicle). To make the scenario interpretable by humans, Anthony uses a logical formalism called signal temporal logic (STL) to control everything in the environment except for the vehicle. Rather than defining STL, I'll show it through an example of an STL expression: "Between 10 seconds and 15 seconds from the start of the simulation, pedestrian #1 will eventually reach 4 mph." This is just the English representation of it, a more formalised representation would look like so:

![The diamond stands for "eventually," \[10, 15\] is the time interval, and x is pedestrian #1's speed.](/images/stl_example.png)

1. describe STL(solution to high dimensionality)
2. describe probability distrbution (solution to unlikely scenarios)
3. describe whole algorithm in easy words

### Stanford Center for AI Safety

### Crux.jl