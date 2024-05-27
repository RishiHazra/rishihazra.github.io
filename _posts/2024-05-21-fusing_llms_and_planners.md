---
layout: post
title: Fusing LLM & Classical Planning
date: 2024-03-20 14:37:00-0400
description:
tags: LLMs Planning
categories: llm-planning
giscus_comments: true
related_posts: true
pretty_table: true
---

In the previous part, the question we asked was: 
**Can we improve LLM planning to have <u>some</u> formal guarantees?**

To answer that, Let's first recap.

|                                    | Classical Planning | LLM Planning  |
|:-----------------------------------|:------------------:|:-------------:|
| **Open-world Planning**            |         ❌          |       ✅       |
| **Handling Abstract Tasks**        |         ❌          |       ✅       |
| **Handling Partial Observability** |         ❌          |       ✅       |
| **Feasibility**                    |         ✅          |       ❌       |
| **Optimality**                     |         ✅          |       ❌       |

<br><br>

We can observe that the formal guarantees come from classical planning. 
Can we somehow combine the best of both? Any guesses? Here's a hint to jog your memories.<br><br>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/thinking_fast_slow.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" style="display: block; margin: auto;" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div><br><br>

Ring any bells now? You guessed it right. <br><br>

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
  <th class="blue-text">Classical Planning</th>
  <th class="pink-text">LLM Planning</th>
</tr>
<tr>
  <td><strong>Open-world Planning</strong></td>
  <td align="center">❌</td>
  <td align="center">✅</td>
</tr>
<tr>
  <td><strong>Handling Abstract Tasks</strong></td>
  <td align="center">❌</td>
  <td align="center">✅</td>
</tr>
<tr>
  <td><strong>Handling Partial Observability</strong></td>
  <td align="center">❌</td>
  <td align="center">✅</td>
</tr>
<tr>
  <td><strong>Feasibility</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
<tr>
  <td><strong>Optimality</strong></td>
  <td align="center">✅</td>
  <td align="center">❌</td>
</tr>
</table><br><br>

Considering <span style="color: cornflowerblue;">LLM Planning</span> as <span style="color: cornflowerblue;">System 1</span> and <span style="color: darksalmon;">Classical Planning</span> as <span style="color: darksalmon;">System 2</span>, we look at two different ways of combining the best of both.
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

### 1. LLMs + external verifiers

### 2. LLMs + external verifiers + heuristic search

### 3. LLMs + dynamics models

---

## LLMs as Knowledge Base for Planners


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
Du, Y. (2023). 
Video Language Planning.
The Twelfth International Conference on Learning Representations.