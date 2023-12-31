# Build Your Own Network Automation Lab

In the first hands-on part of the [Building Network Automation Solutions](https://www.ipspace.net/Building_Network_Automation_Solutions) course, you’ll build your lab and prepare an Ansible environment to control it.

You’ll also create a GitHub account and a local Git repository and publish a file to GitHub (you can also use any other Git-based public repository, for example, GitLab, BitBucket...)

You can work on your own or as a team with your colleagues or other course attendees (in which case, use our Slack team to find them).

## Selecting the Gear

You can build your lab using physical gear or virtual routers, switches, firewalls, or load balancers. To make your job easier, I’d suggest you select equipment you're familiar with that’s supported by [Ansible network modules](http://docs.ansible.com/ansible/list_of_network_modules.html).

Some vendors offer free or evaluation versions of virtual network devices; others offer commercial environments:

- You can download Cumulus VX as a Vagrant box or Docker container.
- You can download Juniper vPTX with zero hassle, but you must build a Vagrant box from the disk image.
- Cisco CSR 1000V, Arista vEOS, and (probably) F5 require registration;
- Cisco VIRL (a commercial product) contains vASA, NX-OS, IOS-XR, IOS-XE, and IOSv.

You’ll also have to set up an environment running Ansible. You could install Ansible on your OSX or Linux workstation or run Ansible in a virtual machine or Docker container.

You’ll find more details in other documents mentioned in the [lab exercise section](https://my.ipspace.net/bin/list?id=NetAutSol&module=1#M1S6).

## Building the Lab

Your lab is ready when you’re able to:

- SSH from your Ansible host to all network devices using usernames/passwords or SSH keys;
- Execute commands on your network devices with the Ansible **raw** module.

## Set up Git and GitHub

After building the lab, it’s time to set up Git and Github:

- Install Git on your workstation;
- Create a Github account;
- Create a new repository on GitHub;
- Create a local copy of that repository [using this recipe](EX-Git_Recipe_Explained.md) (Github has pretty good step-by-step tutorials);

If you’re using Vagrant, create the local repository in a folder shared between your workstation and the virtual machine in which you’re running Ansible.

## Publish a File on GitHub

Finally, publish some content on Github:

- Create a text file describing your lab topology in your local Git repository. Use plain text (.txt) or Markdown.

!!! Tip
    I’m using Visual Studio Code text editor. It has many add-ons, including syntax highlighting for YAML, Jinja2, and Markdown.

-   Commit the changes and push them to Github.

You’ve completed the exercise when you can view the description of your lab topology with a web browser on github.com.
