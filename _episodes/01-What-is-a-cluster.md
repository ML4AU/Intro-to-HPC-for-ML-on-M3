---
title: "What is a cluster?"
teaching: 0
exercises: 0
questions:
- "What is a High Performance Computer (HPC)?"
- "What are the components of a HPC?"
- "What is a scheduler, and why do we need one?"
objectives:
- "Explain what a HPC is at a high level."
- "Explain what a node and scheduler are in a HPC."
- "Determine whether or not HPC is the right tool for your research."
keypoints:
- "Most HPCs are not supercomputers, but clusters composed of many computers."
- "Each computer in the HPC is a group of resources, called a node. Nodes with the same flavour 
  of resources and access requirements are called partitions."
- "A HPC is shared with other people, so it has a scheduler to ensure everyone has fair access."
---

<!---
Prerequisite: None, purely conceptual knowledge here.
Motivations: Understanding what a HPC is will help you determine
if the HPC can assist you with research.
HPC level: 1/5
ML level: 1/5
-->

## What is a HPC?

The acronym HPC refers to a High Performance Computer or High Performance Computing - but what does that really mean?
We will spend some time introducing core terminology here.

- The *cloud* refers to any computing resources which are not right 
  in front of you - remote resources. 
- *Local workstation* in this course will refer to the computer in front of you,
  whether that's a desktop, laptop, tablet, or other device. 
- *Supercomputer* refers to one particular type of high performance computer,
  which is composed of advanced processors. In the past the development of vector 
  processors meant that processor choice alone made a significant difference to the 
  speed at which you could get things done. [CRAY-1](https://doi.org/10.1145/359327.359336) 
  was the first supercomputer implementing these processors. These processors were able
  to complete a single task much faster than the average computer. 
- *Cluster* also refers to a type of high performance computer. Over time, advanced 
  processors have become widely available, so to continue improving performance 
  new techniques were required - having many of these advanced processors and putting 
  them in one "cluster" means that problems that can be distributed across many processors
  can be done in parallel, improving the speed at which you can get things done. 
  Cluster computing is still often referred to as supercomputing.

The HPC we assume you have access to in this course, 
[MASSIVE M3](https://docs.massive.org.au/M3/m3users.html), is a **cluster**.
What this means in practice, is that not all problems are solved faster
simply by running them on a HPC cluster - you have to think about how to adapt your problem
to be distributed accross more processors, or to use the unique hardware like GPUs effectively. 
Don't worry if you're not sure what that looks like yet.

## What are the components of a cluster?
### Nodes
As explained above, a cluster is a collection of "computers".
A single "computer" or group of resources in a cluster is referred
to as a *node*. For example, your local laptop might have 4 CPUs,
16GB of RAM, and no GPUs. 
We can imagine my laptop had identical resources. 
If we could somehow connect our laptops into one cluster, we 
could think of each individual laptop as a node. 

### Partitions
A group of nodes that have the same resources on them, and which
can be accessed by the same group of people, is referred to as a
*partition*. Both of our laptops have the same compute resources,
and can be accessed by both of us, so they would make up a partition.
We can give this partition a name, "no GPU laptops."
If a third person had a laptop with 16 CPUs, 4 GPUs, and 64GB of RAM, 
their laptop would be a new node, but it would belong to a 
different partition. We could call this "4 GPU laptops." 

> ## Why do we need partitions?
>
> Can you think of any reasons it might be helpful to have
> partitions in a cluster? Remember, a partition is just a 
> group of nodes that share some properties.
>
> {: .source}
>
> > ## Solution
> >
> > Organising the cluster with partitions makes it possible to
> > request particular resources based on partition name. It also
> > makes it possible to set certain rules for each partition -
> > for example, you might want a partition that only 
> > allows code that runs for half an hour on it.
> > Grouping those nodes into one partition makes it easier to 
> > organise the cluster and request the right resources.
> > {: .output}
> {: .solution}
{: .challenge}

### Shared filesystem
If I tried to connect our laptops like in our previous example
it would be difficult for both of us to use them.
On my laptop I would only have access to my files,
and on your laptop you would only have access to your files.
On a HPC however, we have a *shared filesystem*, meaning each node,
regardless of partition, has access to the same files.

## Sharing is caring on a HPC
Perhaps the idea of just connecting our laptops
together has already gotten you asking questions about
the challenges of a shared computing system.
However, there are some good motivations for using
a shared HPC, and some tools designed to make sharing
much easier than it would be if we just connected
our personal computers together. 

One motivation for using a HPC is that shared hardware
also means a shared pool of money for buying that hardware.
Computers are expensive - if I only need a GPU sometimes, 
or only need large amounts of storage occassionally, 
it makes sense to split the cost of those resources
across a group of people, and share the resources among them too. 

Of course, when sharing a resource among many people, it's 
important to make sure everyone gets fair access to those resources.
For this reason, when using a HPC you will request 
access to the resources you need, and then a *scheduler*
will decide who gets to use the resources next. This ensures if we
all want to use the same resources at the same time,
there's a method to decide who gets to go first, as 
the scheduler will create a *queue* of all resource requests. 
You can think of the scheduler playing a game of Tetris, where it's trying to fit
all the resource requests together in the best way possible across all the nodes.. 
On M3, our scheduler is called [SLURM](https://slurm.schedmd.com/), which is widely 
used on HPCs. 

> ## How do we make scheduling fair?
>
> Imagine you are the scheduler for a HPC and you 
> have to decide how to order the resource requests.
> What things will help you make your decision?
> How can you make access to the resources fair? 
>
> {: .source}
>
> > ## Solution
> >
> > There are lots of answers to this question.
> > One thing to consider might be if everyone paid
> > the same amount for the hardware. Another might be to 
> > make sure everyone gets access to the same amount of time
> > using the HPC. Another thing to consider is the type of 
> > hardware being requested - if someone asks for 200GB RAM,
> > is it worth the same as someone asking for 20GB RAM, or 500 GB of RAM?
> > It's hard work being a scheduler! The more technical answer to this 
> > question is that the SLURM scheduler uses the Fair Tree Fairshare algorithm to
> > decide how to order the queue, which you can read more about on
> > the [SLURM Website.](https://slurm.schedmd.com/fair_tree.html)
> > {: .output}
> {: .solution}                     
{: .challenge}

