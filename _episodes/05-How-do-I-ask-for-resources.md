---
title: "How do I request resources on the cluster?"
teaching: 0
exercises: 0
questions:
- "What is the difference between login and compute nodes?"
- "How do I request resources on the HPC on the command line?"
- "How do I request resources on the HPC using Strudel2?"

objectives:
- "Submit an interactive job on the command line."
- "Submit a job submission script to the cluster."
- "Query the cluster for information about my jobs."
- "Understand alternative methods to access resources 
  using Strudel2, such as desktops and JupyterLab."
keypoints:
- "The login node should only be used for lightweight
  housekeeping tasks."
- "Interactive jobs are accessed with the smux command on
  MASSIVE and still need to be queued for."
- "Interactive jobs are good for prototyping and developing
  code before submitting jobs."
- "Job submission scripts are an effective and 
  reproducible way to undertake research on the cluster."
- "You can also access MASSIVE resources with desktops and
  JupyterLab sessions using Strudel2."
- "You can interact with running jobs using `squeue`, 
  `scancel`, and `show_job`."
---
<!---
prerequistites: what is a cluster, how do you access,
what resources ar eon the cluster, CLI skills.
HPC: 2/5
ML: 1
motivations: I want compute to do stuff!!!
--->

## Login and Compute Nodes
You have learnt tools to navigate the resources available
to you on the cluster, but we haven't shown you how to 
access those resources yet. In fact, if you look at the 
command prompt that you're logged into to HPC on, it will
say something like [username@m3-login1]. When you login to the cluster, 
rather than putting you on a random node with random 
resources, you're directed to what's called a login node. 
The other nodes which you have seen by using tools like
`sinfo` and `show_cluster`, are referred to as compute nodes.

In general, clusters will have login nodes available. 
It is important to know the login node is shared between
all users who have just logged in, so it should be reserved
for lightweight tasks like opening and editing files,
navigating around the system, submitting jobs, or other
non-computationally intensive tasks. If you run big tasks
on the login node, it will impact other users negatively. 
This means that before you can do computationally 
intensive work like running resnet, you should ask for 
compute node resources, which we will cover shortly. Remember,
the scheduler ensures compute resource access is fair.

> ## When can you use the login node?
>
> Which of the following tasks could be done on the login node?
> 1. Training a neural network
> 2. Downloading a dataset
> 3. Using git to pull a repository
> 4. Editing a script
>
> {: .source}
>
> > ## Solution
> >
> > 1. Training a neural network is computationally intensive,
> >    and may impact other users - don't do this on the login nodes. 
> > 2. Downloading a dataset should also be done on a compute
> >    node, or M3 has a special node for large data downloads
> >    at `m3-dtn.massive.org.au`.
> > 3. A git pull can generally be done safely on the login
> >    node, but if it's particularly large and takes a long
> >    time, consider moving to a compute node instead.
> > 4. Editing a script is lightweight enough that doing this
> >    won't impact other users. You can do this on the login node.
> >
> > In general, if you're not sure if something is too
> > heavy for the login node, request a compute node to run on.
> > {: .output}
> {: .solution}
{: .challenge}

## Requesting compute resources on the command line
Here, we assume you have ssh'd into M3 using a terminal,
or are running a terminal on the login node with Strudel2. 
Traditionally, HPC is accessible via a Linux terminal, so it's
important to understand how to request resources this way,
and how to query the HPC for your requests.

You will remember from earlier than the cluster is shared 
among many users, and so there is a scheduler, and queue. 
*Jobs* refer to tasks for the HPC that wait in the queue, 
including resource requests - you can think of each resource
request as a "job". The way the queue is ordered and the amount
of time you wait to access the resources you ask for is a 
complicated topic that we will discuss later, but for now
you can think of the queue as managing supply and demand.

In general, there are two ways to request resources on the 
command line:
1. Interactively: You get access to a compute node where you can time in commands 
   in real time, the same way you would on your local workstation.
   You may have to wait in the queue to access the compute node interactively.

2. Job submission: You write a list of instructions and 
   send them off the queue in a job submission script, which are
   executed without you actively typing in commands. You may have
   to wait in the queue for your job to start executing, but it
   will execute automatically when resources are available.

There is an additional way to access compute resources on MASSIVE using 
the Strudel interface, which we will cover later. 

## Interactive jobs (srun and smux)
Interactive sessions allow you to connect to a compute node and work on 
that node directly. This allows you to develop how your jobs might run
 (i.e. test that commands run as expected before putting them in a 
script) and do heavy development tasks that cannot be done on the login 
nodes (i.e. use many cores). Despite being interactive, you may need to
queue to gain access to a session.

On a traditional cluster with a SLURM scheduler, you would use the command
`srun` to request resources for and interactive job. On MASSIVE, we have a command
called `smux`, which combines srun with tmux. The command line tool 
`tmux` allows you to reconnect to running sessions, split your terminal
pane so you can do work side by side, and otherwise improve your command
line experience. By combining the two with `smux`, we give you the ability
to connect and reconnect to interactive sessions as they run incase 
your internet drops out in the middle of a job for example. 

In general, the command to start a new interactive job on MASSIVE is 

`smux new-session`

This will request an interactive job with default resources of 1 CPU, 
4G of memory, and 2 hours of walltime. If you run this command, you will
notice your terminal changes and gains a bar down the bottom letting you know
which node you're running on. It will look like this:

IMAGE HERE

This means I'm running on a compute node! 

I can leave this running in the background if I like and exit it by typing
in `Ctrl+b+d`.

I can then reconnect to it while there is remaining walltime by running
smux list-sessions, and then smux attach-session [num]. If I type `exit` or `Ctrl d`,
I'll leave my session and it will be cancelled.If you run `smux list-sessions`
following this, you'll see your session has ended.

There are some parameters you can change in your smux command if you 
need something different than the defaults. For example, you can run

`smux new-session --time=00:03:00`

To update the time from 2 hours to 3 hours. You can see the other parameters 
you're able to change by running smux -h or smux --help, such as ntasks 
(number of CPUs), memory (amount of RAM), or partition (for specific
partitions with certain resources available). 

If you only ask for a small amount of available resources like the default
smux new-session command does, you'll likely not wait at all for your
session to begin. However, if you ask for more than that, you may need 
to wait for your job before you can connect. Every time you request resources 
on the HPC you create a job that waits in the queue, and that job
has an associated job ID. SLURM has a variety of tools for interacting 
with the jobs you're running that work across interactive jobs, jobs 
submitted to the cluster with sbatch, and jobs ran with other tools
such as Strudel Desktops. 

If we type in:

`smux new-session --ntasks=4 --memory=4G --time=24:00:00 --gres=gpu:2`

Now we're asking for many more resources and a resource that's in high
demand with the gres command: a node with a GPU. 
