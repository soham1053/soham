+++
author = "Soham Patil"
categories = ["Interview"]
date = 2021-05-05T02:35:00Z
description = ""
image = "/images/corso-1.jpg"
title = "Anthony Corso: SISL, AI Safety, and Julia"
type = "post"

+++
Anthony Corso is a postdoctoral researcher at the [Stanford Intelligent Systems Laboratory](http://sisl.stanford.edu/ "SISL"), a.k.a. SISL, pronounced "sizzle" :). He wrote his [PhD thesis](http://anthonylcorso.com/wp-content/uploads/2021/02/thesis.pdf "ALGORITHMS FOR BLACK-BOX SAFETY VALIDATION") about algorithms for black-box safety validation of autonomous vehicles, he's the executive director of the [Stanford Center for AI Safety](http://aisafety.stanford.edu/ "Stanford Center for AI Safety"), he wrote a deep reinforcement learning [framework](https://github.com/ancorso/Crux/ "Crux.jl") in Julia, and I recently had the opportunity to speak with him.

### Black-Box Safety Validation

Autonomous vehicles are being hyped more and more nowadays, but how can we ensure their safety? In this chunk of our conversation, we focused on [one part](https://arxiv.org/pdf/2004.06805.pdf "Interpretable Safety Validation for Autonomous Vehicles") of Anthony's thesis: finding relevant scenarios in which to test the vehicle. Anthony worked on a way to generate dangerous scenarios for these vehicles in simulations, so that their safety can be interpreted by humans without risk. Here, black-box means creating scenarios automatically, without the help of humans or manual labor. Firstly, most previous generators produced scenarios too complicated (high dimensional) for humans to interpret or chose scenarios irregardless of how unrealistic they are (imagine a jaguar jumping onto the vehicle).

To make the scenario interpretable by humans, Anthony uses a logical formalism called signal temporal logic (STL) to control everything in the environment except for the vehicle. Rather than defining STL, I'll show it through an example of a very simple STL expression: "Between 10 seconds and 15 seconds from the start of the simulation, a pedestrian will eventually reach 4 mph while walking." This is just the English representation of it; a more formalised representation would look like so:![](/images/stl_example.png). The diamond stands for "eventually," \[10, 15\] represents the time interval, and x is the pedestrian's speed. The simplicity of STL proves it can be interpreted by humans. Also, since "eventually" is vague such that the expression can represent multiple scenarios, scenarios are sampled from STL expressions.

Instead of directly generating scenarios, the algorithm learns to create a probability distribution (represented by some STL expression) over scenarios based on the given likelihood that the scenario happens in real life. By sampling from this, more realistic scenarios will come up more often than unrealistic scenarios.

So how exactly does the learning work? First, a set of STL expressions is sampled from all possible STL expressions. For each expression, a set of scenarios is sampled based on the previously described probability distribution. A cost is computed for each expression, based on how dangerous they are. The STL expressions with the lowest costs are then crossed over and mutated through [genetic programming](https://en.wikipedia.org/wiki/Genetic_programming "Genetic Programming"), with some randomness to allow for exploration. With this new set of expressions, the algorithm loops.

With this, we can now generate realistic dangerous scenarios for testing. Here's an example that was created by the algorithm in an environment where the autonomous vehicle is a pink car: ![](https://ai.stanford.edu/blog/assets/img/posts/2020-08-25-black-box-safety-validation/A2T_failure.gif)

### Stanford Center for AI Safety

> The mission of the Stanford Center for AI Safety is to develop rigorous techniques for building safe and trustworthy AI systems and establishing confidence in their behavior and robustness, thereby facilitating their successful adoption in society.

Anthony's PhD fits right into this mission; by evaluating autonomous vehicles in dangerous situations, society is more willing to adopt AI systems such as self-driving cars. The center strives towards a future of interpretable AI. Most machine learning techniques used today are essentially complex mathematical formulae that map inputs to outputs, and a lot of current techniques can't abstractly reason with us as well as we'd like. 

For example, the Youtube algorithm may have been made to give users the videos that they want or would be useful to them, but for many people, it has ended up giving them videos that are not useful but addicting. This is because the cost function of the Youtube algorithm is likely very weighted on a user's watch time. Being able to reason with AI systems similar to this is crucial to AI safety. 

Some of the main research directions of the Center for AI Safety are formal techniques for AI safety, learning and control, and   transparency. Formal techniques refer to external methods that ensure the safety of conventional software and hardware systems (one example being automatic test-case generation, which Anthony did research in). The learning and control of AI agents out of simulation can be dangerous, so research is being done to ensure their safe exploration and control. AI transparency is critical to AI safety because being able to reason with AI lets us humans decide whether the AI's direct intentions are reasonable.

### Crux.jl

Anthony Corso wrote a library in Julia containing popular deep reinforcement learning algorithms such as [Proximal Policy Optimization](https://arxiv.org/abs/1707.06347) and [Deep Deterministic Policy Gradient](https://arxiv.org/abs/1509.02971). Two intriguing things to talk about here, deep RL and Julia.

Deep RL has been the main talk around reinforcement learning last decade, since it provides a more end-to-end approach for RL problems. Its big kickstart was Deepmind's Nature paper on DQNs in 2015, and has progressed quite far since then, from solving the rubik's cube with a robotic hand to beating the best Dota 2 team. Deep RL is one of the main topics SISL does research in, where the most recent research was in multi-agent control and hierarchical learning.

Although Python is the most popular language in AI today, Anthony and SISL use Julia for its speed and because it's specifically made for statistics and ML. Julia is a multi-paradigm and functional programming language that has the speed of Rust and looks like Python. Most deep RL libraries like OpenAI's Baselines and Tensorforce are on Python, hence the need to expand the RL support for Julia. 

***

Thanks for reading!