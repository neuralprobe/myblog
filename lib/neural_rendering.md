---
layout: page
title: Neural Rendering
description: >
  Render your 3D object to 2D with neural networks
hide_description: true
---

- Table of Contents
{:toc .large-only}

- **SIGGRAPH2021 Course: Adavnces in Neural Rendering** [link](https://www.neuralrender.com/)

## Introduction
- Michael Zollhoefer from Facebook Reality Labs Research
- Two alteratives of realisting image syntehsis
  - Photo-realistic rendering: Lots of manual work + Full control of scene parameter
  - Generative ML: Lots of data + Automatic training + Interactive inference/rendering
- Motivation: Creating photorealistic assets is challenging using classical CG techniques
- Neural Rendering?: 3 Components
  - Generative networks that synthesis raw pixel output
  - Controllable by interpretable parameters or by video/audio input
  - Illumination, camera, pose, geometry, appearance, or semantic structure controllable
- Why neural rendering?: 
  - Can we learn (part of the) scene representation and/or (part of the)  CG function?
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_001.png)
- Neural Rendering Zoo
  - "Regress it" (GQN): 1D code => 2D generative network => 2D image
  - "Make it more real" (DVP, DNR): 3D mesh/points + 1D codes => CG (3D to 2D) => 2D encoder/decoder => 2D image
  - "Regress and render" (Neural volume): 1D code => 2D generative network => 3D mesh/points + 2D texture + 3D volume => CG (3D to 2D) => 2D
  - "Step, sample and blend" (NeRF=super popular in the community): 3D space => Coordinates => MLP => CG (3D to 2D) => 2D image

## Loss functions for nueral rendering
- Jun-Yan Zhu, CMU CS
- Problem statament?
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_002.png)
  - argmin_G Loss(G(x_input),y_output)
  - So, what is a good objective loss function **L**?
- Designing loss function?
  - L2 regression: tends to average out L2-distance, not good for optimize each local image
  - Classificiation loss - Cross entropoy objective with colofulness term
  - Feature/Perceptual loss - Deep feature space matching objective
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_003.png)
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_004.png)
- Loss fucntion in Generative Adversary Network?
  - Distinguish whether it is real of fake image?
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_005.png)
  - Using human annotation is expensive. So replace it with classifier!
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_006.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_007.png)
  - Check pix2pix, edge2cat
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_008.png)
  - What can pix2pix do?
    - grayscale => automatic colorization
    - scatch => photo
    - But, it needs paired training data, which are expensive.
  - Check Cycle-consistent adversarial networks: horse to zebra, orange to apple!
    - How to train with unpaired data (shape of horse + texture of zebra with differnt shape?)
    - Cycle-consistent loss: horse (X) to zebra (G(x)), and zebra to horse again (F(G(x))
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_009.png)
  - Patch-based contrastive loss using cosine similarity of small patches of X and G(X)
  - Summary
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_010.png)

## Generative Adaverial Networks with 3D Control
- Ayush Tewari, Max Planck Institute for Informatics
- GAN?
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_011.png)
- Supervised training of GAN for neural rendering?
  - Add scene prarameters (illumination/pose) to input data and do supervised training
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_012.png)
  - Training with synthetic datasets (so, no need lots of labeled data pairs)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_013.png)
  - Training with supervised pairs? Add annotation tools and move along nomal direction of semantic property (pose/gender/expression) hyperplane in the latent space.
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_014.png)  
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_015.png)
  - Add non-linearity for high quality control!
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_016.png)
  - Inverse graphics & 3D control the semantic property gradually!
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_017.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_018.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_019.png)
- Unsupervised methods?
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_020.png)
  - Training generator for controllability
  - Projecting real images to latent vector using optimziation-based methods
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_021.png)
  - Editing the projected latent vector
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_022.png)
  - Reguralization
  - Transformation
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_023.png)
  - Learning-based methods for projection (not optimization): Using encoder!
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_024.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_025.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_026.png)
- Challenges?
  - What can be edited?: Widen adjustable control parameters!
  - What can be projected?: Trade betwen quality of projection/reconstruction/realistic-editing
- 3D GANs?
  - View points can be controlled explicitly!
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_027.png)

## Neural Scene Representation and Rendering
- Gordon Wetzstein, Stanford EE/CS, [www.computataionlimaging.org](https://www.computataionlimaging.org)
- Self-supervised scene representation learning approach
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_028.png)
- Model 3D object to network network
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_029.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_030.png)
- Then came NeRF: Mildenhall et al., ECCV2020
  - NN is more compact than 3D voxel or mesh
  - Use sirec (periodic fucntion) instead of ReLU
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_031.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_032.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_033.png)
- Pi-GAN
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_034.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_035.png)
- Neural volume rendering is slow! (NeRF, Pi-GAN)
  - Works by defining camera and shooting rays through the scene, and calcuating integrals of each ray (by approaximate integral).
  - Need fast and efficinet integration technique!
  - Not numerical integration, use anti-derivative!
  - AutoInt:
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_036.png)
- Neural lumigraph rendering: real time rending during inference time
- Summary
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_037.png)

## Novel View Syntehsis for Obejcts and Scenes
- Goal: Get 2 images and generate scenes between the two (with arbitraty camera position).
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_038.png)
  - IF you have one image only, then use prior-based reconstruction
- What method?
  - Voxel-based methods: DeepVoxels, Neural Volumns, HoloGAN
  - Neural implicit approaches: Scene representation netowrks, Differentiable volumetric rendering, NeRF, Implicit differentiable renderer
  - Hybrid Implicit/Explicit: Neural sparse voxel fields, PiFU, GRF, pixelNeRF, MVSNerf, Unconstrained scene generation with locally conditioned radiance fields
  - Multi-plane images
  - Image-based: Stable view synthesis, IBRNet
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_039.png)
  - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_040.png)

## Neural Volumetric Rendering: NeRF, etc
- Ben Mildenhall, Google Research ([bmild.github.io](https://bmild.github.io))
- What is nerual volumetric rendering?
  - Rendering?: Querying the radiance value along rays through 3D space
  - Volumetric?: Continuous, differentiable, rendering model without concrete ray/surface intersections 
  - Neural: Using a neural network as a scene representation, rather than a voxel grid of data
  - Inputs: sparse, unstructured, photographs of a scene
  - Outputs: representation allowing us to render new views of that scene
- Volumetric rendering math
  - Traditional method?: using optical pysics => adapted for visualizing medical data and linked alpha compositing => Modern path tracers use sophisticated Monte Carlo methods to render volumetric effects
  - Volumetric redering and ML?: Various volume-rendering-esque methods devised for 3D shape reconstruction methods, scaled up to higher resolution voxel grids, ML methods can achieve excellent view synthesis results.
  - Volumetric formulation for NeRF
    - Scene is a cloud of tiny colored particles
    - If a ray traveling through the scene hits a particle at **t**, we return its color **c(t)**
    - This notion is probabilistic: Chance that ray stops in a small interval around **t** is **sigma(t)dt**. Sigma is known as the "volume density"
    - To determine if **t** is the first hit, need to know **T(t)**: probability that the ray didn't hit any particles earlier. **T(t)** is called "transmittance". We assume **sigma** is known and want to use it to calculate **T**
    - P[no hits before **t**] = **T(t)**
    - P[hit at **t**] = **sigma(t)dt**
    - P[no hits before **t+dt**] = P[no hits before **t**]xP[no hit at **t**]
    - **T(t+dt)** = **T(t)** X **(1-sigma(t)dt)**
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_041.png)
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_042.png)
    - You can weight the intergrand with color function **c(t)**
    - Approaximating the nested integral? Use quadrature to approximate the nested integral, splitting the ray up into **n** segments with endpoints **{t_1,t_2,...,t_(n+1)}** with length **delta_i=t_(i+1)-t_i**.
    - Assume that volume density and color are roughly constant within each interval
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_043.png)
    - Remind that piecewise constant density/color *do not* imply constant transmittance! Important to account for how early part of a segment blocks later part when **sigma_i** is high.
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_044.png)
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_045.png)
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_046.png)
    - Connection to alpha compositing
      - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_047.png)
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_048.png)
    - Next question? How do we store the values of color and sigma at each point in space?
- Neural networks as representations for spatial data 
  - Toy problem: storing 2D image data
    - Usually we stroe an image as a 2D grid of RGB color values
    - What if we train a simple fully-connected network (MLP) to do this instead?
    - Problem: Standard coordinate-based MLPs cannot represwent high frequency functions
    - Solution: Pass input coordinates through a high frequency mapping first
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_049.png)
    - Input coordinate mapping?: Spatial position (x and y) to positional encoding features using sin/cos functions
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_050.png)
    - Scaling frequency matrix B traverses underfitting-overfitting curve. So, optimal scale lies between the extremes.
- Neural Radiance Fields (NeRF)
  - NeRF = Volume rendering + Coordinate-based network
  - Neural network replaces large N-D array
    - (x,y, z, theta, phi) => NN => (r,g,b,sigma)
    - (theta, phi) to visulaize view-dependent effects
    - Train network to reproduce input views of scene using gradient descent 
    - ![img](/assets/img/posts/lib/neuralRendering/neuralrendering_051.png)
- NeRF improvements and extensions
  - NeRF problems
    - Scene representation is not anti-aliased
    - Rendering is very slow: KiloNeRF, FastNeRF ...
    - Network must be retrained for every scene: GRF, IBRNet, pixelNeRF
    - Requires many input images
    - Needs scen to be static and have fixed lighting


   





  