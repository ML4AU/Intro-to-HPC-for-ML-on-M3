---
title: "How do I login to a cluster?"
teaching:
exercises:
questions:
- "How do I log into the cluster?"
- "Are there other methods to log in than the command line?"
- "How do I choose which method to log in?"
objectives: 
- "Log in to MASSIVE M3."
- "Understand login methods available to you."
keypoints:
- ""
---

<!---
prerequisites: CLI Skills; what is a cluster.
HPC skills: 1/5
ML Skills: 1/5
motivation: I have decided I need to use the HPC and need to be able to login.
--->

## Traditional methods: the command line interface
Traditionally, you log into a cluster on the command line, and access the cluster
on the command line as well. Most clusters operate with a Linux operating system
(rather than Windows or Mac)..
As the cluster is a remote resource and not right in front of you, to log in
you will need to secure shell, or `ssh` in.

Whether your local workstation is a Windows, Mac, or Unix
based operating system may impact how you login to the cluster and access the
command line interface, but we will outline instructions for all options here.

### Windows 10
If you're using Windows 10, you should be able to `ssh` into the cluster using
the command prompt.
 
1. Type `cmd` into the search bar, and open the command prompt.
2. In the command prompt, type `ssh username@m3.massive.org.au`, replacing `username` 
with your M3 username. Your username will have been sent
to you in a welcome email, or you can find it in 
[the HPC ID portal](https://hpc.erc.monash.edu.au/).
3. You will be prompted for a password. When you type it in, nothing will 
appear on the screen - this is normal behaviour!
4. Once you have logged in, you will see the message of the day, and the command
prompt should show `[m3username@login1 ~]` or similar.

**Troubleshooting**
- If it's the first time you're logging in, you will get a message asking if
you're willing to accept the cluster's public key. This is one way to confirm
you're logging in to the computer that you think you are, so you don't 
unintentionally send your password somewhere else.  
- If you type your password wrong multiple times, you may be locked out of 
the system and recieve a message saying "Connection reset by peer". 
In this case, wait 10 minutes and try again, or if you've forgotten your password,
reset it in [the HPC ID portal](https://hpc.erc.monash.edu.au/).
- If the command prompt doesn't recognise the `ssh` command, use one of the `Other
Methods` listed here. 

### Mac and Linux
1. Open a terminal.
2. In the terminal, type `ssh username@m3.massive.org.au`, replacing `username`
with your M3 username. Your username will have been sent
to you in a welcome email, or you can find it in
[the HPC ID portal](https://hpc.erc.monash.edu.au/).
3. You will be prompted for a password. When you type it in, nothing will
appear on the screen - this is normal behaviour!
4. Once you have logged in, you will see the message of the day, and the command
prompt should show `[m3username@login1 ~]` or similar.

**Troubleshooting**
- If it's the first time you're logging in, you will get a message asking if
you're willing to accept the cluster's public key. This is one way to confirm
you're logging in to the computer that you think you are, so you don't
unintentionally send your password somewhere else.
- If you type your password wrong multiple times, you may be locked out of
the system and recieve a message saying "Connection reset by peer".
In this case, wait 10 minutes and try again, or if you've forgotten your password,
reset it in [the HPC ID portal](https://hpc.erc.monash.edu.au/).

### Other Methods
Some older Windows computers or some especially fussy computers may have 
trouble using the inbuilt command line to `ssh` into M3. There are other tools available
to help you do this, including:

- PuTTy
- Cygwin
- WinSCP
- The Windows Subsystem for Linux

We'll show you the steps for PuTTY here as it's the most beginner friendly, but 
feel free to try a more advanced option if you're comfortable with `ssh`. 

EXERCISE
Using one of the methods above, ssh into M3.

You have successfully logged in! You will notice that you logged into the cluster
with a password, but it's more secure to log in using keys - keys also save you
from typing in your password every time you access the cluster! There are some instructions 
for setting up an ssh key on docs.massive.org.au here:

## Less traditional methods to access the cluster
On MASSIVE M3, we offer some other methods to access the cluster beyond the command line. 
This includes a desktop interface, JupyterLab, and even a terminal which can be logged into
with your AAF login rather than an `ssh` command.

The benefit of these alternative interfaces is 
they're often more user friendly than the command line, and it enables you to
run visual software on the cluster. M3 isn't the only cluster that provides
access to the cluster via things like desktops - here, we use a tool called
Strudel. 

EXERCISE: LOGIN TO STRUDEL, EXPLORE
