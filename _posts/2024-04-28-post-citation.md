---
layout: post
title: LLMs as Planners?
date: 2024-04-28 15:06:00
description:
tags: formatting citation
categories: sample-posts
citation: true
---

An example of displaying a tweet:
{% twitter https://twitter.com/rubygems/status/518821243320287232 %}

# Timeline

An example of pulling from a timeline:
{% twitter https://twitter.com/jekyllrb maxwidth=500 limit=3 %}


In this blog post, we will address the following question:

### 1. Why?
### 2. Are they really All You Need (for Planning)?

Let's start with 1.

### Open-world Planning

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-1.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/open-world-planning-2.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>


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


### Handling Partial Observability

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/partial-observability-2.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

### What we know so far?

|                                    | Classical Planning | LLM Planning  |
|:-----------------------------------|:------------------:|:-------------:|
| **Open-world Planning**            |         ❌          |       ✅       |
| **Handling Abstract Tasks**        |         ❌          |       ✅       |
| **Handling Partial Observability** |         ❌          |       ✅       |


    So, an LLM is All You Need for Planning. Period. 
    Is it though?

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/well-well.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

### LLMs seem to struggle a bit.

<div class="row">
    <!-- Full width video -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls>
            <source src="/assets/videos/say_final_hanoi.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>

### In fact, it struggles a lot.

<div class="row">
    <!-- Full width video -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls>
            <source src="/assets/videos/say_final_virtualhome.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>

### Even on simple Blocksworld.

<div class="row">
    <!-- Full width image -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <img src="/assets/img/blocksworld.png" width="50%" alt="Description of the image content" class="img-fluid rounded z-depth-1" onerror="this.onerror=null; this.src='image-not-found.png';">
    </div>
</div>

### And neither Prompting, nor Finetuning helps.

So what do we have now?


|                                    | Classical Planning | LLM Planning  |
|:-----------------------------------|:------------------:|:-------------:|
| **Open-world Planning**            |         ❌          |       ✅       |
| **Handling Abstract Tasks**        |         ❌          |       ✅       |
| **Handling Partial Observability** |         ❌          |       ✅       |
| **Feasibility**                    |         ✅          |       ❌       |
| **Optimality**                     |         ✅          |       ❌       |

LLMs are useful for planning. However, there are no formal guarantees.

Can we improve it to have some formal guarantees? 
    Yes