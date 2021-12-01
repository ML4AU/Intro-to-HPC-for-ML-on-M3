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
- Different clusters will have different resources available
  on them.
- You can check resources on the cluster with the command
  line, or by using documentation.
---
<!---
prerequisites: login to cluster, cli, what is a cluster
motivation: I want to know if I can ask for what I need for my problem
HPC: 2/5
ML/ 1/5
--->
So far, you've learned

- What a cluster is
- Why you might want to use one
- How to log into one.

I've told you that there are different resources on a HPC than in your local workstation,
and in this section I'll show you how to find out what's available to you.

## What resources are available in general?
There are a variety of computational resources you may be aware of.
These include:
- CPUs (Central Processing Units). These are designed for
  sequential processing.
- GPUs (Graphical Processing Units). These are traditionally designed for displaying 
  graphics. Graphics are represented with matrices, meaning GPU architecture 
  is excellent at performing matrix multiplications. Some HPC clusters
  will have access to "data center" GPUs, especially designed for computation
  rather than graphics. These will differ from what's typically available to your local workstation.
- TPUs (Tensor Processing Units). These processors have been
  especially designed for working with tensors and neural networks,
  which you may be familiar with from TensorFlow or PyTorch. Notably,
  Google Colab provides access to TPUs, with [an introductory
  tutorial notebook](https://colab.research.google.com/notebooks/tpu.ipynb).  
- Time. When using a HPC you will need to specify how long
  you want to use the shared resources for.
- RAM (Random Access Memory). You will need to consider how much
  memory is required to run your code. 
- Software. Every computer will come with its own unique set of installed
  software - the HPC is included. We'll talk more about specific software later.

> ## Local resources
>
> Take a moment to think about what resources are available on your local workstation. 
> How many CPUs? Do you have a GPU? Any specialised software?
> {: .source}
{: .discussion}


## How do I know what's available on MASSIVE?
There are a variety of methods to discover which resources are 
available to you on a given cluster. Most HPC sites will offer 
a documentation website - for MASSIVE, you can find our documentation on 
[docs.massive.org.au](https://docs.massive.org.au/).
In particular, you can find out more about our hardware on the 
[About M3 page](https://docs.massive.org.au/M3/m3users.html), 
or about our GPUs specifically in 
[our section on GPUs](https://docs.massive.org.au/M3/GPUs-on-M3.html).

We also provide some of this documentation in the 
[Strudel2 interface](beta.desktop.cvl.org.au).
Under the Account Info tab, you are able to see a list of desktop
types that are available, and under the Desktops tab, you will
be able to learn more about the specific resources assigned to each desktop type.

Another method to find out information about the resources on the cluster 
is using the command line. You will remember from "What is a cluster?" that 
we group nodes with the same resources into partitions. Each of these
nodes will have a particular set of resources like CPUs and RAM
associated with it. There are a few ways to learn more about these
partitions and nodes on the command line that we'll explore here. 
Most of these commands are associated with SLURM, the scheduler for our HPC.

### What partitions are available?
- `sinfo -s` : [sinfo is a SLURM command](https://slurm.schedmd.com/sinfo.html)
  that gives you information about nodes and partitions. 
  This particular command summarises the partitions, where 
  the `-s` flag indicates summary. It will output a list of each
  partition, whether it's available at the moment (and not 
  down for maintenance, for example), the time limits or 
  wall time for using that partition, how many nodes are 
  allocated, idle, out, and total, and which nodes belong to
  the partition. 
- `scontrol show partitions` : [scontrol is a SLURM command](https://slurm.schedmd.com/scontrol.html)
  for configuring SLURM, and this command gives you a more 
  in depth view over the partitions available and how they
  have been configured. There may be information in this ouput
  which you don't understand - this is okay, for our purposes
  it's another way of seeing which partitions are on MASSIVE.
  You can also use `scontrol show partition <partition-name>`
  to investigate specific partitions.
### What nodes are available? 
- `sinfo --partition=<partition-name> -N --format=%10N%10c%10m%20f%10G` :
  This sinfo command gives more details about the nodes on 
  a partition. It will print out a list of node names, the number of CPUs, 
  the memory on the node, and any other features such as 
  GPUs.
- `show_cluster` : show_cluster is a command developed for 
  MASSIVE which presents a formatted summary of the status of
  nodes on M3. For a similar output on other clusters, you
  can use `sinfo -lN`. 

> ## Investigating the Cluster
>
> 1. Try typing in the commands above and inspect their
> output. 
> 2. What type of GPUs are there on the m3g partition?
> How did you find out?
>
> {: .source}
>
> > ## Solution
> >
> > 1. There are a variety of formats with different
> > information available to you for learning about the cluster!
> > 2. There are V100 GPUs on the m3g partition. You could
> > have learned this by running:
> > - `sinfo --partition=m3g -N --format=%10N%10c%10m%20f%10G`
> > - `show_cluster`
> > - `sinfo -lN`
> > - Checking docs.massive.org.au for more information 
> >
> > As you can see, there are many ways to learn about the cluster!
> >
> > {: .output}
> {: .solution}
{: .challenge}
