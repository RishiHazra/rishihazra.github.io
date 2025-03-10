---
layout: post
title: Why are LLMs required for Planning?
date: 2024-05-26 15:06:00
description:
tags: LLMs Planning
categories: llm-planning
pretty_table: true
citation: true
---
In my talks, I often encounter a couple of recurring questions. 
The first is **Why** do I use LLMs as Planners in my works? Is it simply because they're the latest rage. Let's be clear -- if you can do something with classical planners -- **don't** use a trillion parameter model for the same? That'd be like throwing a kitchen sink at it. 
However, as we will see, not everything can be *simply* solved using a classical planner. 

Once we tackle that, the inevitable follow-up question arises **Are they all you need for planning**?

These are common questions, and many of us don't have clear answers. Through this blog post, I aim to shed light on these inquiries. 
To kick things off, let's clearly outline the key questions we'll explore:

**Q1. Why are LLMs useful for planning?** 
Why consider LLMs over classical methods? We'll dive into the flexibility and dynamic problem-solving capabilities of LLMs, illustrating how they adapt to new and unforeseen challenges in planning.

**Q2. Are they really All You Need *for planning*?**
Can LLMs meet all your planning needs, or do they have their limitations? We'll critically assess the strengths and potential drawbacks of relying solely on LLMs for planning tasks.


---
## Q1. Why are LLMs useful for planning?<br><br>
### 1. Open-world Planning<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-1.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Here's a scenario: a robot is tasked to deliver a cup for a drink, but the cup is already occupied by tableware. If the robot can't empty the cup itself, what's it to do? Stuck with a predefined domain, a classical planner is restricted to the predefined objects (cups and glasses) it in its [domain file](https://planning.wiki/ref/pddl/domain).

A LLM can draw from its world knowledge to suggest, "How about a bowl?"[[1]](#1) As humans, we know a bowl can function much like a cup — in technical terms, they have similar *affordances*. <br><br>

[//]: # (We will mainly compare LLM Planning with Classical Planning approaches. Classical Planning approaches generally require a predefined [domain file, for e.g. defined in Planning Domain Definition Language &#40;PDDL&#41;&#41;]&#40;https://planning.wiki/ref/pddl/domain&#41;. That is not the case with LLMs. Owing to its internet-scale training, LLMs acquire vast world knowledge that can be utilized to plan in the world. Here's an example where the robot needs to deliver a cup for drinking, however the cup is already occupied by tableware. Let's assume the robot lacks to ability to empty the cup, can it adapt its plan to accommodate another object that is NOT a cup or glass. As humans, we know that a bowl can also be utilized since it has similar *affordances*, however the knowledge of the classical planner is restricted to the confines of the PDDL domain file -- hence, *closed-world*. However, an LLM can utilize its world knowledge for open-world planning [[1]]&#40;#1&#41;. )

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-2.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Take Voyager [[2]](#2), a lifelong learning agent in Minecraft, for example. It's a lifelong learning agent in Minecraft which designs its own *curriculum*, builds a skill library and constantly expands it by interacting with the environment. Each skill is defined in form of executable code blocks and more complex skills are build by composing simpler skills. For e.g., to ``combatZombie``, the agent needs to ``craftStoneSword`` and ``craftShield``, which in turn requires skills like  ``mineWood`` and ``makeFurnace``. 
So how does it work? No points for guessing that the world knowledge of the LLMs come in handy. In contrast, predefining every possible skill and scenario in a classical planner would require extensive knowledge of both the domain and the environment. <br><br>

### 2. Handling Abstract Tasks<br><br>

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
</table><br><br>

Furthermore, LLMs, the veritable know-it-alls, can instantly generate plans for just about any task you can think of, all in *zero-shot* [[3]](#3). Meanwhile, classical planning requires expertly formalized goal conditions in a [PDDL problem file](https://planning.wiki/ref/pddl/problem).<br><br>

[//]: # (As shown in the videos, LLMs can -- in zero-shot --generate plans for any abstractly defined tasks[[3]]&#40;#3&#41;. In contrast, classical planning requires an expert to formally define goal conditions in a [PDDL problem file]&#40;https://planning.wiki/ref/pddl/problem&#41;.)

### 3. Handling Partial Observability<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Classical planners generally work under the assumption of *full observability* modeled via a Markov Decision Process (MDP). Unfortunately, in the real-world, the agent's senors provide only partial information, called *observation*. Such problems are modeled as a Partially Observable MDP (POMDP). At each time step, the sequence of observations made by the agent determines a probability distribution over states of the environment. Such a distribution is called a *belief state*. Needless to say that often leads to intractibility problems as the length of the plan grows.
LLMs can use its world knowledge to handle partial observability. Think of it as a commonsense prior that helps to shape better (posterior) beliefs. For instance, given the task ``make an omlette``, the LLM can output actions to ``go to the fridge`` since eggs are likely to be found in the fridge -- even though eggs are not visible (i.e. partial observation) [[4]](#4).
<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability-2.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Yet another example is where the agent is given the task of ``stacking the lighter block on the heavier block``[[5]](#5). Without the information of weights, a planner will never work. However, a LLM uses *active perception* to first pick up each block to register the weights, then perform the task.
<br><br>

---
## Q2. Are they really All You Need *for planning*?<br><br>

### What we know so far?<br><br>

<table>
<tr>
  <th></th>
 <td><strong>LLM Planning</strong></td>
  <td><strong>Classical Planning</strong></td>
</tr>
<tr>
  <td><strong>Open-world Planning</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Handling Abstract Tasks</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Handling Partial Observability</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
</table><br><br>

Note that these aspects are not outliers -- on the contrary -- these are pretty much the norm in the real-world. 
With LLMs checking all the boxes, it is tempting to declare, **"An LLM is all you need for planning. Period."**
<br><br>
<div class="row">
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/well-well.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
© DALL-E
</div><br><br>

But let's hold that thought. The world of planning doesn't end with these three aspects. 
Are LLMs the be-all and end-all for planning? Maybe not just yet. Let's explore this further and keep our tech enthusiasm in check 😉.
<br><br>

### LLMs seem to struggle a bit [[6]](#6).<br><br>

<div class="row">
    <div class="col-sm-12 col-md-6 offset-md-3 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls style="display: block; margin-left: auto; margin-right: auto;">
            <source src="/assets/videos/say_final_hanoi.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div><br><br>

In the tower of Hanoi setup with just three disks, the LLM outputs infeasible actions.<br><br>


### In fact, it struggles a lot [[6]](#6).<br><br>

<div class="row">
    <!-- Full width video -->
    <div class="col-sm-12 col-md-6 offset-md-3 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls style="display: block; margin-left: auto; margin-right: auto;">
            <source src="/assets/videos/say_final_virtualhome.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div><br><br>

Given the task to ```browse internet```, the LLM generates actions like ```walk stereo``` and ```find bed``` which are irrelevant to the goal.<br><br> 

### Even on simple Blocksworld [[7]](#7).<br><br>

[//]: # (<div class="row">)

[//]: # (    <!-- Full width image -->)

[//]: # (    <div class="col-sm-12 mt-3 mt-md-0">)

[//]: # (        <img src="/assets/img/blocksworld.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">)

[//]: # (    </div>)

[//]: # (</div>)


<div style="text-align: center; width: 50%; margin: auto;">
  {% twitter https://twitter.com/rao2z/status/1624881790212251649 %}
</div><br><br>


### And neither Finetuning[[8]](#8), nor clever Prompting[[9]](#9) helps.<br><br>

* On simple blocksworld, <u>finetuned GPT-3</u> could only solve 122/600 (20%)[[8]](#8).
* GPT-4 could only solve 210/600 (34%) in zero-shot and 214/600 (35.6%) with Chain-of-Thought (CoT) prompting[[8]](#8).
* LLMs perform poorly at verifying solutions (graph colorings[[9]](#9)), hence showing they cannot self-critique and improve.

Comparing to human performance:
* A group of 50 human planners were tested.
* 39 (78%) came up with valid plans.
* 35 (70%) came up with optimal plans.

So what do we have now?<br><br>

<table>
<tr>
  <th></th>
 <td><strong>LLM Planning</strong></td>
  <td><strong>Classical Planning</strong></td>
</tr>
<tr>
  <td><strong>Open-world Planning</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Handling Abstract Tasks</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Handling Partial Observability</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Feasibility</strong></td>
  <td align="center">❌</td>
  <td align="center">✅</td>
</tr>
<tr>
  <td><strong>Optimality</strong></td>
  <td align="center">❌</td>
  <td align="center">✅</td>
</tr>
</table><br><br>

**LLMs are useful for planning. However, there are no formal guarantees.<br><br>**

---

## Is it possible to enhance LLMs to have <u>some</u> formal guarantees? 
<br><br>
Find out in the next installment of our series:
[Fusing LLM and Classical Planning](https://rishihazra.github.io/llm-planning/2024/05/26/fusing_llms_and_planners.html)
<br><br>
<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/Robot_Suspense_PNG.png" width="40%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
© DALL-E
</div><br><br>

---

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

<a id="9">[9]</a> 
Stechly, K. (2023). 
GPT-4 Doesn’t Know It’s Wrong: An Analysis of Iterative Prompting for Reasoning Problems. 
NeurIPS 2023 Foundation Models for Decision Making Workshop