---
title: "What resources are available on the cluster?"
teaching: 0
exercises: 0
questions:
- What resources can I request on a cluster?
- How do I find out which resources are available on the cluster
  I'm using?
objectives:
- Use the command line to determine the resources available on the cluster.
- Use other tools and resources to determine the resources available on the cluster.
keypoints:
- 
---
<!---
prerequisites: login to cluster, cli, what is a cluster
motivation: I want to know if I can ask for what I need for my problem
HPC: 2/5
ML/ 1/5
--->

Now you know what the cluster is and how it may assist your research,
and you have been able to log in. If you have started to think about
the resources you might be able to use for your research, you may
also be wondering how to see if the cluster has what you need.
In this section we will cover a few methods to discover what resources
are available to you on MASSIVE. 

## What resources are available in general?
There are a variety of computational resources you may be aware of.
These include:
- CPUs (Central Processing Units). These are designed for
  sequential processing.
- GPUs (Graphical Processing Units). these are designed for displaying 
  graphics. Graphics are represented with matrices, meaning GPUs 
  are also excellent at matrix multiplications. Some HPC clusters
  will have access to "data center" GPUs, especially designed for this
  type of computation rather than graphical representation. These
  will differ from what's typically available to your local workstation.
- TPUs (Tensor Processing Units). These processors have been
  especially designed for working with tensors and neural networks,
  which you may be familiar with from TensorFlow or PyTorch. Notably,
  Google Colab provides access to TPUs, with [an introductory
  tutorial notebook](https://colab.research.google.com/notebooks/tpu.ipynb).  
- Time. When using a shared cluster environment, one resource you
  will need to specify is how much time you need to access your other
  resources. 
- RAM (Random Access Memory). You will need to consider how much
  memory is required to run your code. 
- MORE? 

## How do I know what's available on MASSIVE?
There are a variety of ways to learn about which resources are 
available to you on a given cluster. Most HPC sites will offer 
a documentation website with information about what's available. 
For MASSIVE, you can find our documentation on [docs.massive.org.au](https://docs.massive.org.au/).
In particular, you can find out more about our hardware on the 
[About M3 page](https://docs.massive.org.au/M3/m3users.html), 
or about our GPUs specifically in [our section on GPUs](https://docs.massive.org.au/M3/GPUs-on-M3.html).

We also provide some of this documentation in the Strudel interface.
Under the Account Info tab, you are able to see a lift of desktop
types that are available, and under the Desktops tab, you will
be able to learn more about those specific GPU resources.

Documentation is one way to find out what is available on the cluster,
but this requires someone to keep it up to date. Another way to 
find out information about the resources on the cluster is using
the command line. You will remember from "What is a cluster?" that 
we group nodes with the same resources into partitions. Each of these
nodes will have a particular set of resources like CPUs and RAM
associated with it. 




