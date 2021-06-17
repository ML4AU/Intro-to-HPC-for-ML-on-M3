---
title: "How do I login to a cluster?"
teaching:
exercises:
questions:
- "How do I log into the cluster?"
- "Are there other methods to log in than the command line?"
- "How do I choose which method to log in?"
objectives: 
- "Log in to MASSIVE M3"
- "Understand login methods available to you."
keypoints:
- ""
---

<---
prerequisites: CLI Skills; what is a cluster.
HPC skills: 1/5
ML Skills: 1/5
motivation: I have decided I need to use the HPC and need to be able to login.
--->
## Traditional methods: the command line interface
Traditionally, you log into a cluster on the command line, and access the cluster
on the command line as well. Most clusters operate in Unix.
As the cluster is a remote resource and not right in front of you, to log in
you will need to secure shell, or ssh in.
FIX ME ADD DETAILS ABOUT SSH
Whether your local workstation is a Windows, Mac, or Unix
based operating system may impact how you login to the cluster and access the
command line interface, but we will outline instructions for all options here.
We've provided a video demonstrating each login method, as well
as written instructions below.

ADD VIDEO HERE
ALSO MAYBE NEST THESE NEXT BITS? 

### Windows 10
If you're using Windows 10, you should be able to ssh into the cluster on the
command line. 
1. Type `cmd` into the search bar, and open the command prompt.
2. On the command prompt, type `ssh username@m3.massive.org.au`, but use your
M3 username instead of the word username. Your username will have been sent
to you in a welcome email, or you can find it in Karaage.
3. You will be prompted for a password. When you type it in, nothing will 
appear on the screen - this is normal behaviour!
4. Once you have logged in, you will arrive at a screen like this.

Troubleshooting:
- If it's the first time you're logging in, you will get a message asking if
you're willing to accept [blah]. Type yes and proceed, this is just to 
confirm you're connecting to what you intend to.
- If you type your password wrong multiple times, you may be locked out of 
the system and recieve a message saying "". In this case, email us at 
help@massive.org.au
- If the command prompt doesn't recognise the ssh command, use one of the other
Windows methods listed here. 

### Other Windows versions
- PuTTY
-Cygwin
-WINSCP
-etc.
### Mac 
- as above
### Linux
- as above

EXERCISE
Using one of the methods above, ssh into M3.

You have successfully logged in! You will notice that you logged into the cluster
with a password, but it's more secure to log in using keys - keys also save you
from typing in your password every time you access the cluster! There is a separate
module to do that located LINK HERE.

## Less traditional methods to access the cluster
On MASSIVE M3, we offer some other methods to access the cluster. This includes
a desktop interface which mimics the desktop environment of a local workstation,
 JupyterLab, and even a GUI (graphical user interface) to
login to the cluster and access the command line, rather than ssh-ing in. 

The benefit of accessing the cluster with these alternative interfaces is 
they're often more user friendly than the command line, and it enables you to
run visual software on the cluster. M3 isn't the only cluster that provides
access to the cluster via things like desktops - here, we use a tool called
Strudel. 

EXERCISE: LOGIN TO STRUDEL, EXPLORE
