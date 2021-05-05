+++
author = "Soham Patil"
categories = ["Reinforcement Learning"]
date = 2021-04-09T02:26:00Z
description = "A brief overview of the fundamentals of reinforcement learning"
image = "/images/reinforcement_learning_basics.jpg"
title = "Reinforcement Learning Overview"
type = "post"

+++
Before we get started on Reinforcement Learning, let's define our problem. The general RL problem is to create some "agent" that acts optimally in some "environment." This might be a bit too general to understand at first, so let's look at an example: the [Snake](https://www.google.com/fbx?fbx=snake_arcade "Snake") game. In this case, the "agent" would be the snake, the "environment" would be the grid, and to play optimally, the snake would have to eat as many apples as possible.

This brings us to Markov decision processes, or MDPs in short.

> Markov decision processes model decision making in discrete, stochastic, sequential environments. The essence of the model is that a decision maker, or agent, inhabits an environment, which changes state randomly in response to action choices made by the decision maker.

\- M.L. Littman

MDPs are models of discrete, stochastic, sequential environments. In the case of the Snake game, the discreteness comes from the fact that there is a finite amount of possible states of the grid, its stochastic nature comes from the random placements of the apples, and it is sequential in the sense that the current state of the grid depends on the previous states. The agent's goal now is to take this MDP and try to get the most "reward," or in the Snake game's example, apples.

Now that we got an overview of what reinforcement learning is trying to do, we can talk about the fun stuff!

### Dynamic Programming

With full knowledge of the MDP(Markov Decision Process), we can train an agent to take optimal actions in the environment. Dynamic programming takes advantage of the fact that MDPs are discrete, and uses that to go through every possible state (look at each possible grid state in Snake), learning how much reward the agent can get from each state (learning that being closer to the apple is good, far away not as good). The agent uses the [Bellman Equations](https://www.youtube.com/watch?v=14BfO5lMiuk "Bellman Equations") to learn.

**Policy Evaluation** - Based on a given policy (agent's strategy), an agent learns how much long term reward it will get from a state using a value(long term reward) function.

**Policy Iteration** - Policy Evaluation with a greedy policy, meaning the policy extracts out the action that will give the greatest value estimate for the next state. 1) The value function evaluates the policy, 2) The policy changes to act greedily to the new value function, 3) repeat.

**Value Iteration** - Uses the Bellman Optimality Equation to find the optimal value function (optimal meaning if the policy function were optimal, the value function would be correct for it). Then, the policy acts greedily and it is then optimal as well.

### Monte Carlo Prediction

Unlike Dynamic Programming, the Monte Carlo method does not have full knowledge of the MDP; rather, all it can do given a policy(agent's strategy) is go through the environment and receive a history of states(like the grid in Snake), actions(up, down, right, left), and rewards(get a reward if the snake ate an apple).

In order to estimate the value function given a policy, the algorithm goes through many episodes(the snake's life) in the environment, and averages out the sum of rewards after each state until the end of an episode.

As the value function updates, the policy updates to be epsilon greedy to the value. This means the policy makes a tradeoff between exploring the environment by taking random actions, and acting greedily to the value function by choosing the action with the highest value estimate.

A problem with Monte Carlo learning is that although it has no bias as it takes the average of every _exact_ total return the agent got from a state, it can have extremely high variance as the total return of one state is based on the remaining rewards of the episode starting at that state, which could be a long line of reward. This means the set of possible lines of rewards would be very large, hence the high variance. The problem with high variance is that in order to learn the policy, the strategy for the agent, the agent would need to learn from a huge amount of data. Luckily, the environment can give us as much data as we want, but it would take a lot of computational power and time given the problem.

### Temporal Difference Prediction

TD Learning is a value estimation method that rather than using total returns to learn its value estimate, uses a method called bootstrapping. This means that instead of finding the total return of one state by going all the way to the end of an episode, we only go a few steps forward in the environment, and estimate the rest with the current value function according to the Bellman Equations. The policy updates in accordance to the value function through the epsilon-greedy strategy like Monte Carlo learning.

###### **Bias-Variance Tradeoff**

Unlike Monte Carlo Learning, TD Learning has low variance, meaning that TD Learning learns much more efficiently(faster and computationally efficient) since Monte Carlo Learning would need to train on many more samples of the environment. However, TD Learning has a lot of bias at the start, and since the value function itself affects its own update, it can lead to a lot of instability in the training.

***

This is about as far as I can go without starting to talk about more niche topics, so feel free to [contact me](mailto:soham1053@gmail.com "contact me") if you want to discuss them or want me to make a post on it. Since this was more of an overview on the basics of RL, I'll drop down some of my favorite resources to dive more deep in the field: [David Silver's RL Course](https://www.youtube.com/watch?v=2pWv7GOvuf0&list=PLqYmG7hTraZBiG_XpjnPrSNw-1XQaM_gB "David Silver's RL Course") (most of my post traces back to this course), Lex Fridman's podcasts with RL researchers, [Open AI's Spinning Up](https://spinningup.openai.com/ "Open AI's Spinning Up").

This post was based on my [GitHub repository of RL notes](https://github.com/soham1053/Learning-Reinforcement-Learning "GitHub repository of RL notes").

More RL and machine learning related posts to come!