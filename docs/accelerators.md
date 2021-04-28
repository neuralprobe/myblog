---
layout: page
title: Domain-Specific Hardware Accelertors
description: >
  describe here
hide_description: true
sitemap: false
---

- Table of Contents
{:toc .large-only}

## Deep learning operations
- A guide to convolution arithmetic for deep learning, Vincent Dumoulin, 2016 [pdf_annotated](/assets/notes/CNNArithmatic.pdf)
- Inception module in GoogLeNet [pdf_annotated](/assets/notes/cs217/Inception_GoogLeNet_Kreview.pdf)


## Review on DL acceleration
- Matrix Computation [link](https://www.amazon.com/Computations-Hopkins-Studies-Mathematical-Sciences/dp/1421407949)
- Efficient Methods and Hardware for Deep Learning, Stanford cs231, Song Han, 2017 [link](http://cs231n.stanford.edu/slides/2017/cs231n_2017_lecture15.pdf)
- Efficient Processing of Deep Neural Networks: A Tutorial and Survey, Sze, MIT [pdf](/assets/notes/Sze_DNN hardware.pdf)
- Tutorial on Deep Learning Acceleration, Vivien Sze, MIT [link](http://www.rle.mit.edu/eems/publications/tutorials/)
- High-Performance Hardware for Machine Learning, W. Dally, 2015 [link](https://media.nips.cc/Conferences/2015/tutorialslides/Dally-NIPS-Tutorial-2015.pdf)
- Acceleration of Deep Learning in Algorithm & CMOS-based Hardware by me (2019)[pdf](/assets/notes/DeepLearningAcc_JHShin.pdf)

## Techniques for DL acceleration
- One weird trick for parallelizing convolutional neural networks, Alex Krizhevsky, 2014 [link](https://arxiv.org/abs/1404.5997)
- BinaryConnect: Training Deep Neural Networks with binary weights during propagations, Matthieu Courbariaux, 2016 [link](https://arxiv.org/abs/1511.00363)
- Measuring the Limits of Data Parallel Training for Neural Networks, J. Lee, Mar. 2019[link](https://ai.googleblog.com/2019/03/measuring-limits-of-data-parallel.html?fbclid=IwAR0o5sHfD83FK3Gp1GvqoiNUpKGbJSszrBb4Ww9lhBQ8RtL18hFj3-AekFo)


## Industrial trend
- BrainWave: Accelerating Persistent Neural Networks at Datacenter Scale, Microsoft, 2017 [link](http://learningsys.org/nips17/assets/slides/brainwave-nips17.pdf)
- TPU: In-datacenter performance analysis of a tensor processing unit, Google, 2017 [link](https://ieeexplore.ieee.org/abstract/document/8192463)
- TPU: Machine Learning for Systems and Systems for Machine Learning, Google, 2017[link](http://learningsys.org/nips17/assets/slides/dean-nips17.pdf)

## Stanford CS217 Reading List (2019)
- Hardware Accelerators for Machine Learning, Stanford cs217 [link](https://cs217.stanford.edu/)
- Is Dark Silicon Useful? by M. B. Taylor, 2012 [pdf_annotated](/assets/notes/cs217/DarkSilicon.pdf)
- Why Systolic Architecture? by H. T. Kung, 1982 [pdf_annotated](/assets/notes/cs217/WhySystolicArchitecture.pdf)
- Anatomy of High Performance Matrix Multiplication by K. Goto [pdf_annotated](/assets/notes/cs217/HighPerformanceMatrixMultiplication.pdf)
- Dark Memory and Accelerator-Rich System Optimization in the Dark Silicon Era by A. Pedram, 2016 [pdf_annotated](/assets/notes/cs217/DarkMemory.pdf)
- TABLA: A Unified Template-based Framework for Accelerating Statistical Machine Learning by D. Mahajan, 2016 [pdf_annotated](/assets/notes/cs217/Tabla.pdf)
- Codesign Tradeoffs for High-Performance, Low-Power Linear Algebra Architectures by A. Pedram, 2012 [pdf_annotated](/assets/notes/cs217/CodesignTradeoffLinAlg.pdf)
- Spatial: A Language and Compiler for Application Accelerators by K. Olukotun, 2018 [pdf_annotated](/assets/notes/cs217/Spatial.pdf)
- Aladdin: A Pre-RTL, Power-Performance Accelerator Simulator Enabling Large Design Space Exploration of Customized Architectures by Y. S. Shao, 2014 [pdf_annotated](/assets/notes/cs217/Aladdin.pdf)
- Roofline: An Insightful Visual Performance Model
for Floating-Point Programs and Multicore Architectures by D. Patterson [pdf_annotated](/assets/notes/cs217/RooflineVyNoYellow.pdf)
- In-Datacenter Performance Analysis of a Tensor Processing Unit by Google [pdf_annotated](../wifi/cs217/TPUv1.pdf)
- NVIDIA TESLA V100 GPU ARCHITECTURE [pdf_annotated](/assets/notes/cs217/volta-architecture-whitepaper.pdf)
- Efficient Processing of Deep Neural Networks: A Tutorial and Survey by V. Sze [pdf_annotated](/assets/notes/cs217/2017_sze_dnn.pdf)
- A Systematic Approach to Blocking Convolutional Neural Networks by M. Horowitz [pdf_annotated](/assets/notes/cs217/systolicCNN.pdf)
- Eyeriss: A Spatial Architecture for Energy-Efﬁcient Dataﬂow for Convolutional Neural Networks [pdf_annotated](/assets/notes/cs217/2016_isca_eyeriss_architecture.pdf)
- Brooks' DL for computer architecture, See Chapter 5 [pdf_annotated](/assets/notes/cs217/DLforarchitecture.pdf)
- High Performance Zero-Memory Overhead Direct Convolutions by T. Low [pdf_annotated](/assets/notes/cs217/ZeroMemOverheadDirectConv.pdf)
- Fast Algorithms for Convolutional Neural Networks (Winograd) by A. Lavin [pdf_annotated](/assets/notes/cs217/FastConv.pdf)
- CATERPILLAR: Coarse Grain Reconfigurable Architecture for Accelerating the Training of Deep Neural Networks by A. Pedram [pdf_annotated](/assets/notes/cs217/Catepillar.pdf)
- SCALEDEEP: A Scalable Compute Architecture for Learning and Evaluating Deep Networks by A. Raghunathan [pdf](/assets/notes/cs217/ScaleDeep.pdf)
- Simon Knowles: Designing Processors for Intelligence [video](https://www.youtube.com/watch?v=7XtBZ4Hsi_M&feature=youtu.be)
- An overview of gradient descent optimization algorithms [link](http://ruder.io/optimizing-gradient-descent/)
- LARGE BATCH TRAINING OF CONVOLUTIONAL NETWORKS by Y. You [pdf](/assets/notes/cs217/LargeBatchCNN.pdf)
- DSD: DENSE SPARSE DENSE TRAINING FOR DEEP NEURAL NETWORKS by S. Han [pdf](/assets/notes/cs217/DSD.pdf)
- High-Accuracy Low-Precision Training by C. D. Sa [pdf](/assets/notes/cs217/HALP.pdf)
- EIE: Efficient Inference Engine on Compressed Deep Neural Network by S. Han [pdf](/assets/notes/cs217/EIE.pdf)
- A Cloud-Scale Acceleration Architecture by Microsoft [pdf](/assets/notes/cs217/CloudScaleAccelerationArchitecture.pdf)
- Serving DNNs in Real Time at Datacenter Scale with Project Brainwave by Microsoft [pdf](/assets/notes/cs217/BRAINWAVE_.pdf)
- DAWNBench: An End-to-End Deep Learning Benchmark and Competition by M. Zaharia [pdf](/assets/notes/cs217/nips_sysml_dawnbench.pdf)
- MLPerf: A broad ML benchmark suite for measuring performance of ML software frameworks, ML hardware accelerators, and ML cloud platforms [link](https://mlperf.org/)
- REVISITING SMALL BATCH TRAINING FOR DEEP NEURAL NETWORKS by C. Luschi [pdf](/assets/notes/cs217/SmallBatch.pdf)
- NIPS 2017 Workshop: Deep Learning At Supercomputer Scale [link](https://supercomputersfordl2017.github.io/)
- DEEP GRADIENT COMPRESSION: REDUCING THE COMMUNICATION BANDWIDTH FOR DISTRIBUTED TRAINING by W. Dally [pdf](/assets/notes/cs217/DeepGradientCompression.pdf)
- Plasticine: A Reconfigurable Architecture For Parallel Patterns by K. Olukotu [pdf](/assets/notes/cs217/plasticine-isca2017.pdf)
- Applied Machine Learning at Facebook: A Datacenter Infrastructure Perspective by Faceboo [pdf](/assets/notes/cs217/hpca-2018-facebook.pdf)





