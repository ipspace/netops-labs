# Easy Wins: Create Summary Reports

We’ll keep the first encounter with Ansible and Ansible playbooks simple: you’ll develop a playbook to collect information from your network and create a report based on the collected data.

Regardless of what problem you decide to solve or how hard you want your task to be, you’ll probably follow these steps:

- Define the problem (what do you want to report)
- Figure out how to get the information from the network devices
- Define the report format
- Create and test the playbook that collects the information and generates the report
- Write documentation
- Publish your solution to your Github account.

## Simple Reports

Assuming you’ve created the Ansible inventory file to solve the [previous assignment](EX-Build_Lab.md), your playbook doesn’t have to be more complex than this:

- Collect information from the host using SNMP (using **snmp\_facts**), REST API, or CLI commands returning JSON format (example: **nxos\_command** with **output** set to **json**), or device-specific facts (**ios\_facts**, **nxos\_facts**, **junos\_facts**…). Using traditional CLI commands will make your job harder;
- Store the collected information in text files or create a summary report based on the information.

Here are a few problems you could solve with this approach:

-   Create a summary report listing device software version, uptime, memory utilization, interfaces, or IP addresses or subnets
-   Collect MAC or ARP information from your devices and store it into text files (one per device) or use it to create a summary report.
-   Create a hardware inventory report (assuming the devices you use in your lab return that information in an easy-to-use format).
-   Verify that all devices in your network have DNS and NTP servers configured;

## More Advanced Reports

Here are a few ideas if you’re looking for a more challenging task:

-   Parse CLI printouts in Ansible or Python filter, or use NAPALM or `ntc-ansible` modules to collect the information;
-   Collect the list of IP addresses from devices, create a sorted list of subnets in your network, and list routers/interfaces/IP addresses in each subnet.
-   Collect MAC and ARP information from your devices and create a summary report sorted by MAC addresses.
-   Verify that all interfaces on which HSRP (or VRRP) is configured have an operational HSRP (or VRRP) neighbor.

## Data Manipulations and Interesting Templates

If you want to practice your Jinja2 templating skills or try out data manipulation in Ansible, solve one of these challenges:

-   Collect network topology using information from LLDP, OSPF, or BGP neighbors, and create a network diagram (hint: use GraphViz DOT or D2 file format);
-   Collect device IP addresses and create DNS zone file and (advanced part) reverse DNS zone file.

## Supporting Materials

Useful tools:

-   [Live Jinja2 parser/renderer](http://jinja.quantprogramming.com/) is a great way to get started

You’ll probably find these videos from the [*Ansible for Networking Engineers*](https://my.ipspace.net/bin/list?id=AnsibleOC) materials useful:

- Baseline Ansible skills are covered in [*Using Ansible*](https://my.ipspace.net/bin/list?id=AnsibleOC#ANSIBLE) section (in particular the *Introduction to Ansible* and *Ansible Playbooks* videos).
- You might want to watch *working with files* video in [*Ansible Deeper Dive*](https://my.ipspace.net/bin/list?id=AnsibleOC#ANSIBLE_DD) section.
- The [*Ansible Networking Modules – Executing Commands*](https://my.ipspace.net/bin/list?id=AnsibleOC#NET_CMD) section describes Ansible modules you’ll use to gather data and various ways of collecting information from networking devices.
- If you want to generate a summary report from a template, you’ll have to be familiar with Jinja2 – watch the [*Creating Templates with Jinja2*](https://my.ipspace.net/bin/list?id=AnsibleOC#JINJA2) section.
- Jinja2 [whitespace control](http://jinja.pocoo.org/docs/dev/templates/#whitespace-control) could get interestingly complicated - check out [whitespace handing in Jinja2](https://my.ipspace.net/bin/get/Ansible/J6%20-%20Whitespace%20Handling%20in%20Jinja2.mp4?doccode=AnsibleOC).
