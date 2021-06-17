---
title: "Why should I use a HPC?"
teaching: 0
exercises: 0
questions:
- "What does a cluster have that my local workstation doesn't?"
- "What problems are clusters good at solving?"
- "What machine learning specific problems can a cluster help me solve?"
objectives:
- "Outline resources available on a cluster compared to your 
  existing local workstation."
- "Identify if your research problems are suited to the HPC environment."
- "Describe problems within machine learning that are suitable for 
   the HPC environment."
keypoints:
- "HPCs offer increased resource size across storage, RAM,
  the number of CPUs, the number and type of GPUs, as well as 
  the ability to perform parallel computing."
- "A HPC may assist you in speeding up your research, but it's 
  important to spend some time identifying where it can assist
  your research problem, or modifying the problem to suit the HPC environment."
- "Deep learning in particular lends itself to the HPC environment,
  and can accelerate your training."
---
<!---
Prerequisite: What is a cluster?  
Motivations: Understanding what problems are suitable on the HPC
allows you to decide whether or not to continue this course :)
HPC level: 1/5
ML level: 2/5
-->  

## So, why would I use a HPC?
Remember, that not all problems are solved faster by using a cluster.
If all I do is move my code from my local workstation onto the HPC, 
I may not see any improvement at all - you have to spend some time
thinking about what you can benefit from the HPC. 
Some reasons you might use a HPC, particularly for machine learning, are:
- The HPC has resources that you don't have - for example, your personal
  workstation might not have any GPUs for your GPU enabled code.
- The HPC has better versions of resources you do have, like GPUs
  with more RAM available, enabling you to use bigger batch sizes.
- The HPC has more storage available than your local workstation,
  enabling you to work on bigger datasets.
- You have code that runs for a very long time, and want to outsource
  that work off of your local workstation.
- You have code which can be scaled across multiple CPUs or GPUs,
  and want to takw advantage of the cluster to scale your code.
Usually, someone moves to the HPC when they realise they're being limited
by their existing computational equipment.

> ## Research restriction
>
> Can you think of a time when your research was limited by your
> computing resources, or when something was more difficult than
> it needed to be?
>
> {: .source}
>
> > ## Answers
> >
> > There are many good answers to this question - maybe your 
> > code was too slow or you couldn't download a whole dataset.
> > Write your 
> > problem down and at the end of this course, see if you can
> > solve it. 
> >
> > {: .output}
> {: .solution}
{: .challenge}

## What problems are HPCs good at solving?
- A HPC can't do *sequential* problems extra fast. For example,
  when you get ready in the morning, you can't brush your teeth
  and eat breakfast at the same time, they must be done in order.
- A HPC can distribute your work if you can break it into parts 
  that don't depend on or conflict with other parts. For example,
  you can have toast in the toaster and a kettle boiling  
  at the same time.
- Long story short - if your problem can be broken into independant 
  parts, a HPC may help accelerate your work. Sometimes this takes
  some thinking and work to achieve. 

## Matrix Multiplication with Friends
A concrete example of a problem which can be decomposed into 
parts is matrix multiplication.

If we were to multiply two 2x2 matrices by hand, it would look like:

[[a,b]  [[e,f],  = [[ae+bg, af+bh],
 [c,d]]  [g,h]]     [ce+dg, cf+dh]]

Let's suppose that every multiplication takes 1 second, and every
addition takes 1 second. Each of the four components of our new 
matrix, (i.e. ae+bg) is comprised of two multiplications, and 1 addition, meaning
it takes each component 3 seconds to calculate. If we do this alone,
it would take us 12 seconds to calculate the resulting matrix.

However, there are a few ways we could share this problem with friends.
We know each component takes two multiplications and one addition,
but the multiplications can be done independantly. We can do the multiplications 
simultaneouslt if there are two people working, calculating each matrix 
component in two seconds, and the entire matrix in 8 seconds. 

We can also see each component of the matrix can be worked out 
independantly - if we had 8 people working on the matrix at once,
two per individual component, we could calculate the result in just 2 seconds. 
By decomposing our work into independant pieces and doing them simultaneously, 
we can reduce computation time from 12 seconds to only 2! 

> ## Parallel Problems
>
> Can you think of any other problems, in mathematics, 
> or your day to day life, that can be parallelised if you have
> more people to work on them?
>
> {: .discussion}

## What ML problems is a HPC suitable for?
Access to a HPC is useful for a variety of machine learning problems.
Some examples of where a HPC excels in machine learning include:
- In deep learning specifically, there is a lot of matrix multiplication.
  GPUs are designed to handle graphical representation, which 
  means they're able to effectively accelerate the matrix operations  
  associated with deep learning. Some HPCs provide more advanced 
  GPUs designed for computation rather than graphics, which are
  especially good for this task.
- When developing a machine learning model, there is a need to test
  out hyperparamaters. This often means running the same model multiple
  times with different hyperparameters, or doing a grid search
  to determine those ideal hyperparameters. These tests can be 
  performed independantly of eachother, but your local workstation
  may be limited by the number of processes it has - you can access
  more of these on a HPC.
- Similarly, when evaluting the performance of a model, you may use
  techniques like cross-validation, which require repeated independant
  runs of the same code. Having more processors to distribute
  this workload across simultaneously is where a HPC comes in handy.
