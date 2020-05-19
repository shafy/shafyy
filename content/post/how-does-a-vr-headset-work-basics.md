---
title: "How does a VR headset work? The Basics"
date: 2020-03-10T21:50:00+00:00
draft: false
---

In this article, I want to give you a quick overview of the basics that make a modern VR headset tick. It doesn't get too technical.

I'm going to focus on 6 degrees of freedom (DoF), stand-alone (also called mobile, or all-in-one) VR headsets such as the Oculus Quest or the HTC Vive Focus. These are headsets that don't need a PC or external sensors to run. Of course, a lot of the technology in stand-alone and PC VR headsets are similar. The main difference is that PC VR headsets rely on the CPU and GPU of the connected computer to do the heavy lifting, and therefore are more powerful. In stand-alone headsets, everything is done on-board.

Here's a quick overview of the basic components that make a VR headset tick.

# CPU, GPU and battery

A VR headsets contains a lot of parts that other computers (such as laptops and smartphones) also contain. The basic components of a computer are the CPU (central processing unit) and a memory to store data. Like most modern computers, VR headsets also contain a GPU (graphics processing unit) that helps to increase performance when displaying images. Which, obviously, is quite important for a VR headset. For example, the Oculus Quest's CPU is a Qualcomm Snapdragon 835 and its GPU is a Qualcomm Adreno 540 GPU. [1]

Stand-alone headsets also need a on-board power source, so they contain Lithium-ion batteries.

# Optical lenses and screens

Unlike the 2D screens we are used to on our laptops and phones, a VR headset needs our eyes and brain to think that we are in a different 3D virtual world. This is done with optical lenses.

Fundamentally, VR headsets use normal screens. For example, the Quest has an OLED screen, while the Oculus Rift S has an LCD screen. That screen is located only a couple of centimeters in front of your eyes, but the lenses distort the photons that are emitted from the screen, changing the path of the light and the angle that hit your eyes. Your brain uses a variety of cues to orient itself in space. VR headsets simulate these cues to create the feeling of immersion.

Depending on the the screen, the lenses and the distance from your eyes, the produced image will have a different resolution and field of view (FoV). In this case, it makes more sense to measure the angular resolution or Pixel Per Degree (PPD) instead of only the resolution of the screen behind the lenses. This is what ultimatly matters to your eyes. Simply said, given a fixed resolution, a headset with a smaller FoV has more PPD. Obviously there are more factors that determine image quality. This simple example shows that designing VR headsets is a never ending game of trade-offs (in this case, FoV vs. PPD).

For example the Oculus Quest has a binocular horizontal FoV of about 95° (binocular meaning when you look with both eyes) and a horizontal resolution of 1440 pixels. Therefore, the horizontal PPD is 15 [2]

# Tracking

6 DoF headsets need to know your position and your rotation in 3D space so that they can move you in the virtual world you are seeing accordingly. The six in 6 DoF comes from the fact that there are three degrees of freedom related to translation, and three related to rotation (translation and rotation around x, y, and z axes in 3D space).

Until not so long ago, headsets had to rely on external sensors for positional tracking. Newer stand-alone headsets like the Oculus Quest don't need that. Rather, they use cameras that are integrated in the headset. With advances in machine learning, specifically computer vision, it is now amazingly possible to get enough positional information from the cameras. Simply said, based on the camera images, the headset knows where you are in a room and how you move through it. Furthermore, it also knows where your controller and hands are, and knows it well enough to use that information to represent them seemlessly in VR. In addition to cameras, other types of sensors such as accelerometers and gyroscopes are used.

# Software

Finally, there's some serious software wizardry going on to bring everything together and produce the final images your eyes see and go "OMG, is this real?". This includes dozens of different pieces of software, from low level code running on the controllers and components of the headset, to higher level code that make the final calculations to get the output just right.
Stand-alone headsets are extremely resource-constrained, meaning that they need to produce great results with a smaller GPU, CPU and less power than their PCVR counterparts. Here, software plays an important role in optimizing the usage of the given hardware. Recently, there has been a lot of progress in this area, especially with the advancement of machine learning. For example, Oculus uses machine learning to increase the resolution of produced images without using more GPU time or power [3].


Obviously, there are many more parts that make up a VR headset and one could fill a huge number of pages for each one of them. In this post, I gave an overview of the components that I think are the most interesting and important ones. In future posts, I will focus on single topics mentioned here, describing and explaining them in more technical detail.

Questions? Join in the discussion on [Twitter](https://twitter.com/canolcer/status/1237496747871567880).

<br />
*Sources:*

1: https://developer.oculus.com/quest

2: https://en.wikipedia.org/wiki/Comparison_of_virtual_reality_headsets

3: https://ai.facebook.com/blog/using-integrated-ml-to-deliver-low-latency-mobile-vr-graphics


