---
layout: post
title: LLMs as Planners?
date: 2024-04-28 15:06:00
description:
tags: formatting citation
categories: sample-posts
citation: true
---

In this blog post, we will address the following question:

### 1. Why?
### 2. Are they really All You Need (for Planning)?

Let's start with 1.

### Open-world Planning

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-1.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

We will mainly compare LLM Planning with Classical Planning approaches. Classical Planning approaches generally require a predefined [domain file, for e.g. defined in Planning Domain Definition Language (PDDL))](https://planning.wiki/ref/pddl/domain). That is not the case with LLMs. Owing to its internet-scale training, LLMs acquire vast world knowledge that can be utilized to plan in the world. Here's an example where the robot needs to deliver a cup for drinking, however the cup is already occupied by tableware. Let's assume the robot lacks to ability to empty the cup, can it adapt its plan to accommodate another object that is NOT a cup or glass. As humans, we know that a bowl can also be utilized since it has similar *affordances*, however the knowledge of the classical planner is restricted to the confines of the PDDL domain file -- hence, *closed-world*. However, an LLM can utilize its world knowledge for open-world planning [[1]](#1). 

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-2.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

Yet another example is Voyager [[2]](#2), a lifelong learning agent in Minecraft, which by designing its own *curriculum*, builds a skill library and constantly expands it by interacting with the Minecraft environment. Each skill is defined in form of executable code blocks and more complex skills are build by composing simpler skills. For e.g., to ``combatZombie``, the agent needs to ``craftStoneSword`` and ``craftShield``, which in turn requires skills like  ``mineWood`` and ``makeFurnace`` No rewards for guessing that the world knowledge of the LLMs come in handy. The methods leads to quite advance and complex minecraft behaviour. To preemtively define all skills (including unexpected scenarios) in a classical planner requires expert knowledge of the domain and also the environment.

### Handling Abstract Tasks

<table>
  <tbody>
    <tr>
      <!-- Video 1 -->
      <td align="center" valign="top" width="25%">
        <video width="100%" controls>
          <source src="/assets/videos/organize_closet.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
        <br /><sub><b>Organize Closet</b></sub>
      </td>
      <!-- Video 2 -->
      <td align="center" valign="top" width="25%">
        <video width="100%" controls>
          <source src="/assets/videos/browse_internet.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
        <br /><sub><b>Browse Internet</b></sub>
      </td>
      <!-- Video 3 -->
      <td align="center" valign="top" width="25%">
        <video width="100%" controls>
          <source src="/assets/videos/turn_off_tv.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
        <br /><sub><b>Turn off TV</b></sub>
      </td>
    </tr>
  </tbody>
</table>

As shown in the videos, LLMs can -- in zero-shot --generate plans for any abstractly defined tasks[[3]](#3). In contrast, classical planning requires an expert to formally define goal conditions in a [PDDL problem file](https://planning.wiki/ref/pddl/problem).

### Handling Partial Observability

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

Classical planners generally work under the assumption of *full observability* modeled via a Markov Decision Process (MDP). Unfortunately, in the real-world, the agent's senors provide only partial information, called *observation*. Such problems are modeled as a Partially Observable MDP (POMDP). At each time step, the sequence of observations made by the agent determines a probability distribution over states of the environment. Such a distribution is called a *belief state*. Needless to say that often leads to intractibility problems as the length of the plan grows.
LLMs can use its world knowledge to get handle partial observability. Think of it as a commonsense prior that helps to better (posterior) belief state. For instance, given the task ``make an omlette``, the LLM can output actions to ``go to the fridge`` since eggs are likely to be found in the fridge -- even though eggs are not visible (i.e. partial observation) [[4]](#4).

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability-2.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

Yet another example is where the agent is given the task of ``stacking the lighter block on the heavier block``[[5]](#5). Without the information of weights, a planner will never work. However, a LLM uses *active perception* to first pick up each block to register the weights, then perform the task.

### What we know so far?

|                                    | Classical Planning | LLM Planning  |
|:-----------------------------------|:------------------:|:-------------:|
| **Open-world Planning**            |         ❌          |       ✅       |
| **Handling Abstract Tasks**        |         ❌          |       ✅       |
| **Handling Partial Observability** |         ❌          |       ✅       |


Note that these aspects are not outlier -- on the contrary -- these are pretty much the norm in the real-world. Now that I have managed to convince you that LLMs are required for real-world planning, what next?  An LLM is All You Need for Planning. Period. 
Is it though? Let's not get ahead of ourselves ;)

<div class="row">
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/well-well.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

### LLMs seem to struggle a bit [[6]](#6).

<div class="row">
    <div class="col-sm-12 col-md-6 offset-md-3 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls style="display: block; margin-left: auto; margin-right: auto;">
            <source src="/assets/videos/say_final_hanoi.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>


### In fact, it struggles a lot [[6]](#6).

<div class="row">
    <!-- Full width video -->
    <div class="col-sm-12 col-md-6 offset-md-3 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls style="display: block; margin-left: auto; margin-right: auto;">
            <source src="/assets/videos/say_final_virtualhome.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>

### Even on simple Blocksworld [[7]](#7).

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/blocksworld.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

{% twitter https://twitter.com/rao2z/status/1624881790212251649 %}

### And neither Prompting, nor Finetuning helps [[8]](#8).

* 50 human planners
* 39 (78%) came up with valid plan
* 35 (70%) came up with optimal plan
* <u>Finetuned-GPT3</u> could only solve 20% (122 out of 600)

So what do we have now?


|                                    | Classical Planning | LLM Planning  |
|:-----------------------------------|:------------------:|:-------------:|
| **Open-world Planning**            |         ❌          |       ✅       |
| **Handling Abstract Tasks**        |         ❌          |       ✅       |
| **Handling Partial Observability** |         ❌          |       ✅       |
| **Feasibility**                    |         ✅          |       ❌       |
| **Optimality**                     |         ✅          |       ❌       |

LLMs are useful for planning. However, there are no formal guarantees.

### Can we improve it to have <u>some</u> formal guarantees? 
    Yes


## References
<a id="1">[1]</a> 
Ding, Y. (2023). 
Integrating action knowledge and LLMs for Task Planning and situation handling in open worlds. 
Autonomous Robots, 47, 981-997.

<a id="2">[2]</a> 
Wang, G. (2024). 
Voyager: An Open-Ended Embodied Agent with Large Language Models. 
Transactions on Machine Learning Research, 2835-8856.

<a id="3">[3]</a> 
Huang, W. (2022). 
Language Models as Zero-Shot Planners: Extracting Actionable Knowledge for Embodied Agents. 
Proceedings of the 39th International Conference on Machine Learning, PMLR 162:9118-9147.

<a id="4">[4]</a> 
Vemprala, S. (2023). 
ChatGPT for Robotics: Design Principles and Model Abilities.

<a id="5">[5]</a> 
Sun, L. (2023). 
Interactive Planning Using Large Language Models for Partially Observable Robotics Tasks.

<a id="6">[6]</a> 
Hazra, R. (2023). 
SayCanPay: Heuristic Planning with Large Language Models Using Learnable Domain Knowledge. 
Proceedings of the AAAI Conference on Artificial Intelligence, 20123--20133.

<a id="7">[7]</a> 
Valmeekam, K. (2023). 
PlanBench: An Extensible Benchmark for Evaluating Large Language Models on Planning and Reasoning about Change. 
NeurIPS 2023 Track on Datasets and Benchmarks.

<a id="8">[8]</a> 
Kambhampati, S. (2023). 
On the Role of Large Language Models in Planning. 
ICAPS 2023 Tutorial