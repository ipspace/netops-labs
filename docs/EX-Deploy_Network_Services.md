# Deploy Network Services From a Data Model

In this hands-on assignment, you'll create, deploy, and validate network device configurations using the [infrastructure and services data model created in the previous hands-on assignment](EX-Create_Service_Data_Model.md).

You might decide to work on a single platform or implement a multi-platform or multi-vendor solution. Regardless of your end goal, start with a single-platform implementation and gradually extend it (which also means that you should start with a multi-vendor framework to avoid bloated code or extensive code refactoring when adding multi-platform support).

If you work in a team, try splitting the multi-platform work across team members (each member working on a different platform) to get hands-on integration experience.

## Before You Start

This hands-on assignment can turn into a massive project; you can easily spend a man-week or more to get it done. Hopefully, you’ll eventually do it, but if you’re short on time, trim it down to a manageable size. Regardless of where you decide to stop, write short documentation, commit the changes and push them to GitHub (or another public repository you’re using), and [submit the solution](http://my.ipspace.net/bin/course/submit?doccode=NetAutSol&module=4).

The first step is the very minimum you should complete: create device configurations and deploy them on your lab devices. Ideally, you'd also check the infrastructure deployment (LLDP neighbors, BGP neighbors, etc.). Those with more time should tackle the initial network services deployment task first and then proceed to the full-blown services project.

## Create Initial Device Configurations

Using the data from node- and infrastructure data models, create initial device configurations using Jinja2 templates and deploy them on devices in your lab. If your devices support **configuration, replace** functionality, use that; otherwise, make sure the device configurations you create are *idempotent* (nothing gets deployed when you deploy the same configuration the second time).

You can complete the job using the Ansible network device configuration management modules, NAPALM, or simple device commands (copy file to the device, replace configuration…).

## Validate Infrastructure Configurations

After deploying infrastructure-related device configuration, validate successful deployment by checking interface state, LLDP, OSPF, or BGP neighbors.

Many devices can return the data you need for validation in a structured format that’s easy to convert to Ansible facts; use NAPALM to simplify information gathering if your lab includes Cisco IOS devices.

## Deploy Initial Network Services

-   Extend the initial solution to create network services configuration;
-   Use **configuration replace** functionality to deploy the services;
-   Validate correct deployment of network services.

While the rest of the assignment is optional, I’d highly recommend you complete it, as you’ll often have to work in an ill-defined brownfield environment where the following approach is the only one with a reasonable chance of success.

## Incremental Services Deployment

Modify the network services deployment solution to deploy services incrementally (by adding them to the device configurations instead of replacing whole configurations).

**Step 1:** Start with a simple solution that generates target device configuration based on service definition, deploys the configuration, and validates correct service deployment.

**Step 2**: Add support for service removal – add configuration commands to remove any service marked with **state: absent**.

**Step 3**: Check the device state before configuring the services and reject the change if it overwrites an existing service. For example, reject adding a device into a VRF if it already belongs to another VRF (another customer).

**Step 4:** Report extraneous services – list all target services (example: all VRFs) configured on a device, compare them to the expected list of configured services, and report any discrepancies.

**Step 5**: Automatic cleanup – automatically remove all unexpected services found on the network devices.

## Useful Links

- [Managing network services configuration with Ansible](https://my.ipspace.net/bin/get/NetAutSol/DOC-Managing-Network-Services-Ansible.md)

Sample projects:

-   [Routing and MPLS infrastructure deployment](https://github.com/ipspace/MPLS-infrastructure)
-   [VLAN services management](https://github.com/ipspace/VLAN-service) (check out various branches to explore stages in the project development)
-   [OSPF deployment](https://github.com/ipspace/ansible-examples/tree/master/OSPF-Deployment)
-   [Network automation tutorial](https://github.com/dravetech/network-tutorials) by David Barroso
