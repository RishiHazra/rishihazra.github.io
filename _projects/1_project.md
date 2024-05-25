---
layout: page
title: Natural Language-based Robotic Planning and Manipulation
description: Object Detection, Planning with Large Language Models, Plan Execution and In-Hand Pose Estimation
img: /assets/img/robot-saycanpay.jpg
importance: 1
category: work
related_publications: saycanpay
---

<div class="row">
    <!-- Full width video -->
    <div class="col-sm-12 mt-3 mt-md-0">
        <video class="img-fluid rounded z-depth-1" controls>
            <source src="/assets/videos/wasp-proj-ppt-low-res.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </div>
</div>


This project aims to develop a robotic pick-and-place system that generates plans in natural language and executes object placement in specific poses, addressing complex constraints found in industrial assembly tasks. A key task example involves placing objects by specified shape and color into corresponding containers. The system is divided into detection, planning, and in-hand perception and control modules. These work in tandem to identify object properties, generate step-by-step plans from natural language inputs, and adjust the robot arm's movement to ensure objects are correctly oriented to match container specifications. 
Each module has been integrated into a complete proof-of-concept system that demonstrates the feasibility of visual reasoning for pick and place, including in-hand perception to account for uncertainty in the attained grasp configuration.

The planning system uses Large Language Models while performing tree-search over actions from the paper [SayCanPay: Heuristic Planning with Large Language Models using Learnable Domain Knowledge](https://rishihazra.github.io/SayCanPay/).