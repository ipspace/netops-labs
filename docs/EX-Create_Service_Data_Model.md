# Data Models: Create a Service Data Model

In the hands-on part of the [*Data Models*](https://my.ipspace.net/bin/list?id=NetAutSol&module=3) module, you’ll build a comprehensive set of data models describing your devices, network infrastructure, and a sample service.

To build the data model, start by listing the attributes you need to describe:

-   Your nodes (device name, loopback IP address…)
-   Common network parameters (usernames, standard servers…)
-   Infrastructure (links, routing protocols…)
-   Service you want to model (customers, ports, port parameters, service parameters…).

You can build a data model for any network infrastructure and service you like. Here are a few examples:

- Internet access service;
- Managed IPsec VPN service;
- Managed firewall service (or firewall access lists);
- VLANs across a data center fabric (implemented with VXLAN, EVPN+VXLAN, TRILL, FabricPath…)
- L2VPN or L3VPN service across an MPLS-enabled IP core.

## Select the Data Store(s)

After grouping the attributes into these four categories, decide how to represent these parameters and where to store them. For example:

- Node-specific parameters will be stored in per-node YAML files in the **host\_vars** directory. Alternatively, store all node-specific parameters in a single **nodes.yml** file.
- Common network parameters will be stored in the **group\_vars/all.yml** file… or you could store them in the **network.yml** file and include variables from that file into your playbook.
- Infrastructure parameters will be stored in the **fabric.yml** file.
- The service model will be stored in the **services.yml** file.

## Abstract the Data Models

Try to make the infrastructure and service data models as simple as possible and hide the underlying network complexity in the *business logic* (configuration templates).

For example:

- Define links in your network, not individual ports on devices;
- Define IP prefixes on links (or use unnumbered links), not IP addresses on device ports;
- If you’re running a single routing protocol in your network, don’t specify routing protocol parameters in the data model unless absolutely necessary.

Likewise, the service data model should be service-oriented rather than device-oriented. For example:

- Don’t specify transport technologies (for example, VXLAN or DMVPN) in the service definition.
- Specify each service as a list of devices and ports on which that service should be configured, plus a few service-specific parameters (service name, VLAN ID, MPLS/VPN RT/RD…).

## Sample Data Models

You’ll find sample infrastructure- and service data models in:

* [Network Automation Data Model Optimization](https://blog.ipspace.net/kb/DataModels/)
- *Abstract everything* section of [Network Automation Use Cases](https://my.ipspace.net/bin/list?id=NetAutUC) webinar;
- David Barroso’s [Network Tutorials](https://github.com/dravetech/network-tutorials) and [Ansible Demo](https://github.com/dbarrosop/ansible_demo) repositories;
- [DHCP Pools](https://github.com/ipspace/ansible-examples/tree/master/DHCP-Pools) example (simple data store used to create local DHCP pools on Cisco IOS routers)
- [OSPF Deployment](https://github.com/ipspace/ansible-examples/tree/master/OSPF-Deployment) - fabric data model with LLDP validation and fabric-to-node translation;
- [MPLS Infrastructure](https://github.com/ipspace/MPLS-infrastructure) - full-blown fabric- and services data models with OSPF, BGP, and MPLS/VPN deployment;
- [VLAN service deployment](https://github.com/ipspace/VLAN-service) - complete service deployment solution using a service data model to describe customer connectivity needs (= VLANs).

## Documentation

Describe your data model (attributes, required values…) in a text file, and include that text file in your GitHub repository. It doesn’t matter how you describe your data model – the description must be concise enough to enable someone else to add new nodes, infrastructure components (links), or services.

Sample data model descriptions are included with these examples:

- [Manage DHCP pools](https://github.com/ipspace/ansible-examples/tree/master/DHCP-Pools)
- [Deploy IGP+BGP routing in a multi-AS MPLS/VPN network](https://github.com/ipspace/MPLS-infrastructure/)

## Validate the Data Model

Build simple Jinja2 templates that will generate relevant parts of device configurations from your data model to verify that you’ve included all pertinent parameters or that they’re easy to derive from the data in the data model.

For example, it’s easy to generate node IP addresses if your data model includes infrastructure links defined like this – the left node gets the first IP address in the subnet, and the right node gets the second IP address.

    - left: E1
      left_port: GigabitEthernet0/2
      right: E2
      right_port: GigabitEthernet0/2,
      subnet: 10.0.0.20/30
      cost: 5

Sometimes, you might figure out that working with your data model in the configuration templates is hard. In that case, it might be better to insert an extra step and transform your service-oriented data model into a node-oriented one.

## More information

You’ll find several useful Jinja2 templates that work with abstracted infrastructure and services data models in David Barroso’s [Network Tutorials](https://github.com/dravetech/network-tutorials) and [Ansible Demo](https://github.com/dbarrosop/ansible_demo) repositories;

These documents will help you transform your data model:

- [Data munging with Ansible and Jinja2](https://my.ipspace.net/bin/get/NetAutSol/DOC-Data_Munging_Ansible_Jinja2.md)
- Playbooks in the [MPLS Infrastucture](https://github.com/ipspace/MPLS-infrastructure) and [VLAN Service](https://github.com/ipspace/VLAN-service) repositories (use [this URL](https://github.com/ipspace/VLAN-service/tree/VLAN_Data_Model) to get the simplest version of the VLAN services project that includes data model transformation)
- [OSPF Deployment](https://github.com/ipspace/ansible-examples/tree/master/OSPF-Deployment) example
