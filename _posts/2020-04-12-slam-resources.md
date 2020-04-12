---
title: "Resources to Master SLAM and Visual Odometry"
date: 2020-04-12
mathjax: true
tags: ["computer vision", "slam","visual odometry"]
---

The ability for a computer to automatically and intelligently understand its environment has always been fascinating to me. One computer vision technique developed in the last two decases that has made large strides towards this goal is Simultaneous Localization and Mapping (SLAM). SLAM is a powerful computer vision framework that is not only powering today's Augmented Reality(AR) Headsets, but also powering society's most exciting cutting edge technologies such as robotics and autonomous vehicles. 

[![ARKit](https://media.giphy.com/media/RrAqQNvF54DgQ/giphy.gif)](https://media.giphy.com/media/RrAqQNvF54DgQ/giphy.gif)

[![Tesla Autopilot](https://www.carscoops.com/wp-content/uploads/2020/01/Tesla-Autopliot.gif)](https://www.carscoops.com/wp-content/uploads/2020/01/Tesla-Autopliot.gif)


The first gif is ARKit, an iOS framework thatimplements Augmented Reality using its own proprietary monocular slam system. The second gif is a demo of Tesla Autopilot, a software system that integrates SLAM with object detection to autonomously manuver on the road.

What is complicated is how to implement and understand. SLAM is a complex, niche technology that is still an active area of research and combines topics in robotics, computer vision, and optimization. 

The goal of this post is to share amazing resources I have found that compiles all the key components to implementing your own SLAM and what I will start reading to hopefully implement my own SLAM system! As there are many resources on youtube and papers, these resources I believe will help anyone get started and implement and learn SLAM!

# Table of Contents
- [What is SLAM](#what-is-slam)
- [Resources to Learn SLAM](#resources-to-learn-slam)
  * [Textbook: 14 Lectures on Visual SLAM: From Theory to Practice](#textbook-14-lectures-on-visual-slam-from-theory-to-practice)
  * [Monocular Visual Odometry using OpenCV](#monocular-visual-odometry-using-opencv)
  * [Exploring RGBD Odometry](#exploring-rgbd-odometry)
- [Github projects](#github-projects)
  * [twitchslam](#twitchslam)
  * [OpenCV-RgbdOdometry](#opencv-rgbdodometry)
  * [An Invitation to 3D Vision: A Tutorial for Everyone](#an-invitation-to-3d-vision-a-tutorial-for-everyone)
- [Off-the-shelf tools](#off-the-shelf-tools)
  * [RGBD Visual Odometry and 3D reconstruction: Open3D](#rgbd-visual-odometry-and-3d-reconstruction-open3d)

# What is SLAM
Simultaneous Localization and Mapping (SLAM) is a framework that enables a computer, with only a camera sensor and movement, to simultaneously understand its orientation in 3D space. It is a multi-stage pipeline where the goal is to take a sequence of images, and generate a 3d map of the camera moving in 3D space. The pipeline comprises of visual odometry, back-end filters & optimization, loop closing, and Reconstruction. The input to a SLAM system is a sequence of images (either livestreamed or froma video), and the output is 3D position/orientation of the camera and a map (whether 3d map or a topological map) of the environment.

{% capture fig_img %}
![Slambook]({{ "/images/slam-resources/SLAM_framework.jpeg" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>SLAM Framework, photo from slambook-en.</figcaption>
</figure>


# Resources to Learn SLAM

## Textbook: 14 Lectures on Visual SLAM: From Theory to Practice
Recenetly I discovered this amazing textbook 14 Lectures on Visual SLAM: From Theory to Practice, written byXiang Gao and Tao Zhang and Yi Liu and Qinrui Yan.
<img src="{{ site.url }}{{ site.baseurl }}/images/slam-resources/slambook-title.png" alt="linearly separable data">

 This textbook is a compiled end-to-end introduction in to visual SLAM. The book is broken down in a 12 part series, and includes C++ code walkthroughs to develop your own SLAM system! The original textbook is written in chinese, but the author is also providing an english translation here [https://github.com/gaoxiang12/slambook-en](https://github.com/gaoxiang12/slambook-en). The book is not fully translated, but [se7oluti0n](https://github.com/gaoxiang12/slambook-en/issues/15) took the liberty to translate the rest of book using google translate! View here to snag the entire translated book here: [https://github.com/se7oluti0n/slambook-en/blob/master/slambook-en.pdf](https://github.com/se7oluti0n/slambook-en/blob/master/slambook-en.pdf) 

 Link to the original implementation: [https://github.com/gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)

## Blogs

### Monocular Visual Odometry using OpenCV
[https://avisingh599.github.io/vision/monocular-vo/](https://avisingh599.github.io/vision/monocular-vo/)
Written by Avish Singh, the author implements the first component of a visual slam framework, called visual odometry. Visual Odometry basically extracts unique image features from an image, tracks those features over the next consecutive image, and calculates the relative position and orientation of the camera. This blogpost is great because its written in OpenCV and source code is shared here: [https://github.com/avisingh599/mono-vo](https://github.com/avisingh599/mono-vo)

Checkout the demo of the code:
<iframe width="560" height="315" src="https://www.youtube.com/embed/homos4vd_Zs" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Monocular Visual and Inertial Odometry
Blog by dattadebrup [https://dattadebrup.github.io/monocular/inertial/odometry/2018/07/23/Monocular-Visual-and-Inertial-Odometry.html](https://dattadebrup.github.io/monocular/inertial/odometry/2018/07/23/Monocular-Visual-and-Inertial-Odometry.html)

<iframe width="560" height="315" src="https://www.youtube.com/embed/2coEdSWuACA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Exploring RGBD Odometry
Blog by dattadebrup. [https://dattadebrup.github.io/rgbd/depth/odometry/2018/08/02/Exploring-RGBD-Odometry.html](https://dattadebrup.github.io/rgbd/depth/odometry/2018/08/02/Exploring-RGBD-Odometry.html)

{% capture fig_img %}
![Slambook]({{ "/images/slam-resources/RGBD_img.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>SLAM using RGBD, photo from slambook-en.</figcaption>
</figure>

## Github projects

### twitchslam 
 [https://github.com/geohot/twitchslam](https://github.com/geohot/twitchslam)

 {% capture fig_img %}
![Slambook]({{ "/images/slam-resources/example.png" | relative_url }})
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>output of twitchslam, photo from https://github.com/geohot/twitchslam</figcaption>
</figure>

### OpenCV-RgbdOdometry
 [https://github.com/tzutalin/OpenCV-RgbdOdometry/](https://github.com/tzutalin/OpenCV-RgbdOdometry/)
[![Demo video](https://j.gifs.com/lYEqx5.gif)](https://www.youtube.com/watch?v=NS2L7_uHTAo&feature=youtu.be)
### An Invitation to 3D Vision: A Tutorial for Everyone
[https://github.com/sunglok/3dv_tutorial](https://github.com/sunglok/3dv_tutorial)

Beginner tutorial on basic theory of 3D vision and implement their own applications using [OpenCV]. Example code is also provided! The example codes are written as short as possible (mostly __less than 100 lines__) to be clear and easy to understand.

* [tutorial slides](https://github.com/sunglok/3dv_tutorial/releases/download/misc/3dv_slides.pdf)

## Off-the-shelf tools

### RGBD Visual Odometry and 3D reconstruction: Open3D
Slightly related topic to SLAM is 3D reconstruction. 3D reconstruction utilizes visual odometry, however rather than focusing on creating a 3D map reconstruction, 3D reconstruction focuses on consolidating 3D point clouds into a final 3D model. 
[http://www.open3d.org/docs/release/tutorial/ReconstructionSystem/index.html#reconstruction-system](http://www.open3d.org/docs/release/tutorial/ReconstructionSystem/index.html#reconstruction-system)