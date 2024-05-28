---
layout: post
title: Fusing LLM & Classical Planning
date: 2024-05-26 14:37:00
description:
tags: LLMs Planning
categories: llm-planning
giscus_comments: false
related_posts: true
pretty_table: true
citation: true
---

In the previous part, the question we asked was: 
**Can we improve LLM planning to have <u>some</u> formal guarantees?**

To answer that, Let's first recap.
<style>
  /* Color the header of the second column blue */
  .blue-text {
    color: cornflowerblue;
  }

  /* Color the header of the third column pink */
  .pink-text {
    color: darksalmon;
  }
</style>

<table>
<tr>
  <th></th>
  <th class="pink-text">LLM Planning</th>
  <th class="blue-text">Classical Planning</th>
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

We can observe that the formal guarantees come from classical planning. 
Can we somehow combine the best of both? Any guesses? Here's a hint to jog your memories.<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/thinking_fast_slow.png" width="40%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Ring any bells now? You guessed it right. <br><br>

Considering <span style="color: darksalmon;">LLM Planning</span> as <span style="color: darksalmon;">System 1</span> and <span style="color: cornflowerblue;">Classical Planning</span> as <span style="color: cornflowerblue;">System 2</span>, we look at two different ways of combining the best of both.
* Equip LLMs with verifiers, dynamics, and heuristic search.
* Use LLms as knowledge bases for open-world planning
<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/classical_plus_llms.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

---

## LLMs + verifiers, dynamics, and heuristic search.<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/verify_step_by_step.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Let's first start with some motivation. [[1]](#1) shows that:
* LLMs can generate *good* solutions if called multiple times.
* Verifiers help discard *bad* candidate actions/plans.<br><br>

### 1. LLMs + external verifiers<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/saycan.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/SayCanPay/resources/saycanpay_teaser.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

### 2. LLMs + external verifiers + heuristic search<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/SayCanPay/resources/decoding_strategies.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

### 3. LLMs + dynamics models<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/llms_as_world_models.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/video_language_planning.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>


---

## LLMs as Knowledge Base for Planners<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/llm_p.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/hierarchical_planning.png" width="80%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>


---

Perhaps, a more apt conlusion would be:

A Large Language Model *(+ a Solver)* is All You Need!<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/llm-modulo.png" width="70%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

---


## References
<a id="1">[1]</a> 
Lightman, H. (2023). 
Let's Verify Step by Step.

<a id="2">[2]</a> 
Ahn, M. (2022). 
Do As I Can, Not As I Say: Grounding Language in Robotic Affordances.
6th Annual Conference on Robot Learning

<a id="3">[3]</a> 
Hazra, R. (2023). 
SayCanPay: Heuristic Planning with Large Language Models Using Learnable Domain Knowledge. 
Proceedings of the AAAI Conference on Artificial Intelligence, 20123--20133.

<a id="4">[4]</a> 
Hao, S. (2023). 
Reasoning with Language Models is Planning with World Models.
Proceedings of the 2023 Conference on Empirical Methods in Natural Language Processing, 8154--8173.

<a id="5">[5]</a> 
Du, Y. (2024). 
Video Language Planning.
The Twelfth International Conference on Learning Representations.

<a id="6">[6]</a> 
Liu, B. (2023). 
LLM+P: Empowering Large Language Models with Optimal Planning Proficiency.

<a id="7">[7]</a> 
Wong, L. (2024). 
Learning Grounded Action Abstraction from Language.
The Twelfth International Conference on Learning Representations