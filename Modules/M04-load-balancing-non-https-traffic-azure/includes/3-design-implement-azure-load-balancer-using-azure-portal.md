# Design and implement Azure Load Balancer using the Azure portal

**Azure Load Balancer** operates at layer 4 of the Open Systems Interconnection (OSI) model. It's the single point of contact for clients. Azure Load Balancer distributes inbound flows that arrive at the load balancer's front end to backend pool instances. These flows are according to configured load-balancing rules and health probes. The backend pool instances can be Azure Virtual Machines or instances in a virtual machine scale set.

## Choosing a Load Balancer Type

Load balancers can be public (a.k.a. external) or internal (a.k.a. private).

A [**public load balancer**](https://docs.microsoft.com/en-us/azure/load-balancer/components) can provide outbound connections for virtual machines (VMs) inside your virtual network. These connections are accomplished by translating their private IP addresses to public IP addresses. External load balancers are used to distribute client traffic from the internet across your VMs. That internet traffic might come from web browsers, module apps, or other sources.

An [**internal load balancer**](https://docs.microsoft.com/en-us/azure/load-balancer/components) is used where private IPs are needed at the frontend only. Internal load balancers are used to load balance traffic from internal Azure resources to other Azure resources inside a virtual network. A load balancer frontend can also be accessed from an on-premises network in a hybrid scenario.

![Picture 2](../media/load-balancer.png)

 

## Supporting High Availability with Azure Load Balancer

To achieve high availability with Azure Load Balancer, you can choose to use availability sets and availability zones to ensure that virtual machines are always available. Combine the Azure Load Balancer with an availability zone or availability set to get the most application resiliency.

### Availability sets

An availability set is a logical grouping that you use to isolate virtual machine resources from each other when they're deployed. Azure ensures that the virtual machines you put in an availability set run across multiple physical servers, compute racks, storage units, and network switches. So, if there's a hardware or software failure, only a subset of your virtual machines is affected, while your overall solution stays operational. In this way, availability sets are essential for building reliable cloud solutions. It is recommended that two or more VMs are created within an availability set to provide for a highly available application and to achieve a 99.95% Azure Service Level Agreement (SLA).

Each virtual machine in your availability set is assigned an update domain and a fault domain by the underlying Azure platform. Each availability set can be configured with up to three fault domains and twenty update domains. Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time. When more than five virtual machines are configured within a single availability set, the sixth virtual machine is placed into the same update domain as the first virtual machine, the seventh in the same update domain as the second virtual machine, and so on. The order of update domains being rebooted may not proceed sequentially during planned maintenance, but only one update domain is rebooted at a time. A rebooted update domain is given 30 minutes to recover before maintenance is initiated on a different update domain.

![Picture 1](../media/availability-sets-configuration.png)

 

**Availability sets can be used by Basic load balancers and Standard load balancers (see next section).**

### Availability zones

Availability zones are unique physical locations within an Azure region, and they offer groups of one or more datacenters that have independent power, cooling, and networking. The virtual machines in an availability zone are placed in different physical locations within the same region. To ensure resiliency, there's a minimum of three separate zones in all enabled regions. This physical separation of availability zones within a region protects applications and data from datacenter failures. Zone-redundant services replicate your applications and data across availability zones to protect them from single-points-of-failure. With availability zones, Azure provides a 99.99% VM uptime SLA.

You would typically use this architecture when you want to ensure that, when an entire datacenter fails, you can continue to service your users' requests.

![Picture 2](../media/availability-zones-configuration.png)

Azure services that support availability zones fall into three categories:

- Zonal services: Resources can be pinned to a specific zone. For example, virtual machines, managed disks, or standard IP addresses can be pinned to a specific zone, which allows for increased resilience by having one or more instances of resources spread across zones.

- Zone-redundant services: Resources are replicated or distributed across zones automatically. Azure replicates the data across three zones so that a zone failure does not impact its availability. 

- Non-regional services: Services are always available from Azure geographies and are resilient to zone-wide outages as well as region-wide outages.

**Availability zones do not support all sizes of virtual machine and are not available in all Azure regions. You should check that they are supported in your particular region before you use them in your architecture.**

**Availability zones can be used by Standard load balancers but are not supported for use in Basic load balancers (see next section).**

## Selecting an Azure Load Balancer SKU

Two SKUs are available when you create a load balancer in Azure: Basic load balancers and Standard load balancers. These SKUs differ in terms of their scenario scope and scale, features, and cost. Any scenario that is possible with the Basic load balancer can also be created with the Standard load balancer.

To compare and understand the differences, review the table below.

| *Features*                     | **Basic Load Balancer SKU**                                  | **Standard Load Balancer SKU**                               |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Backend pool size**          | Supports up to 300 instances                                 | Supports up to 1,000 instances                               |
| **Backend pool endpoints**     | Virtual machines in a single availability  set or virtual machine scale set | Any virtual machines or virtual machine  scale sets in a single virtual network |
| **Health probes**              | TCP, HTTP  Does not support secure HTTP (HTTPS)              | TCP, HTTP, HTTPS                                             |
| **Health probe down behavior** | TCP connections stay alive on an instance  probe down. All TCP connections end when all probes are down | TCP connections stay alive on an instance  probe down **and** on all probes  down |
| **Availability Sets**          | Supported                                                    | Supported                                                    |
| **Availability Zones**         | N/A                                                          | Zone-redundant and zonal frontends for  inbound and outbound traffic |
| **Diagnostics**                | Azure Monitor logs                                           | Azure Monitor multi-dimensional metrics                      |
| **HA ports**                   | N/A                                                          | Available for Internal Load Balancer                         |
| **Secure by default**          | Open by default. Network security group  optional            | Closed to inbound flows unless allowed by  a network security group. Internal traffic from the virtual network to the  internal load balancer is allowed |
| **Outbound Rules**             | N/A                                                          | Declarative outbound NAT configuration                       |
| **TCP Reset on Idle**          | N/A                                                          | Available on any rule                                        |
| **Multiple front ends**        | Inbound only                                                 | Inbound and outbound                                         |
| **Management Operations**      | 60-90+ seconds typical                                       | Most operations < 30 seconds                                 |
| **Service Level Agreement**    | N/A                                                          | 99.99% for 2 or more VMs                                     |



**Microsoft recommends Standard load balancer. Standalone VMs, availability sets, and virtual machine scale sets can be connected to only one SKU, never both. Load balancer and the public IP address SKU must match when you use them with public IP addresses. **

**SKUs aren't mutable; therefore, you cannot change the SKU of an existing resource. **



## Creating and Configuring an Azure Load Balancer

There are several tasks you need to perform to successfully create and configure an Azure Load Balancer. 

### Create the load balancer

In this example, we are looking at the tasks required to create and configure a **Public** (external) **load balancer** in a **Basic SKU**. The first task is to create the load balancer itself.

From the Azure portal home page, select **Create a resource**.
![Picture 13](../media/create-load-balancer-1.png)

On the Create a resource page, you can either browse to try and find the resource type you want to create or enter your search criteria in the search box and press ENTER. For example, type **Load Balancer**. To narrow down the search results, you can use the filters to the right of the search box. For example, select **Publisher Type**, and then choose **Microsoft**. 
![Picture 14](../media/create-load-balancer-2.png)

Then choose the **Load Balancer** resource from Microsoft.
![Picture 15](../media/create-load-balancer-3.png)

On the Load balancer page, choose **Create** to start the process.
![Picture 16](../media/create-load-balancer-4.png)

On the **Create load balancer** page, you must supply the following required information:

- **Subscription** - select the Azure subscription that you want to create your new load balancer resource in.

- **Resource group** - here you can select an existing resource group or create a new one.

- **Name** - provide a unique name for the instance.

- **Region** - select the region where the virtual machines were created.

- **Type** - this is where you select whether your load balancer is going to be **Internal** (private) or **Public** (external). If you choose **Internal**, you will need to specify a virtual network and IP address assignment, but if you choose **Public**, you will need to specify several Public IP address details. 

- **SKU** - here you can select either the **Standard** SKU or the **Basic** SKU (for production workloads you should choose **Standard**, but for testing and evaluation and training purposes, you could choose **Basic**, but you will not get all the possible load balancer features). Depending on which SKU you select here, the remaining configuration options will differ slightly.

- **Tier** - this is where you select whether your load balancer is balancing within a region (**Regional**) or across regions (**Global**) - If you select the **Basic** SKU above, this setting is greyed out.

- **Public IP address** - here you specify whether to create a new public IP address for your public-facing front-end, or use an existing one, and you also specify a name for your public IP address, and whether to use a dynamic or statically assigned IP address. You can optionally also assign an IPv6 address to your load balancer in addition to the default IPv4 one.

![Picture 17](../media/create-load-balancer-5.png)

After you click **Review + Create**, the configuration settings for the new load balancer resource will be validated, and then you can click **Create** to start creating it. 
![Picture 18](../media/create-load-balancer-6.png)

The resource will start to be deployed.
![Picture 19](../media/create-load-balancer-7.png)

![Picture 20](../media/create-load-balancer-8.png)

When it completes, you can click **Go to resource** to view the new load balancer resource in the portal.

![Picture 21](../media/create-load-balancer-9.png).

 

### Add a backend pool

The next task is to create a backend pool in the load balancer and then add your virtual machines to it.

From the Azure portal home page, select **All resources**.

![Picture 12](../media/create-backend-pool-1.png)

Select your load balancer from the list.

![Picture 22](../media/create-backend-pool-2.png)

Under the **Settings** section choose **Backend pools**, and then **Add** to add a pool.

![Picture 24](../media/create-backend-pool-3.png)

You need to enter the following information on the **Add backend pool** page.

| **Field**       | **Information**                                              |
| --------------- | ------------------------------------------------------------ |
| Name            | Enter a unique name for the backend pool.                    |
| Virtual network | Specify the name of the virtual network where the resources are located that you will be adding to the backend pool. |
| Associated to   | You need to associate the backend pool with one or more virtual machines, or to a virtual machine scale set. |
| IP Version      | Select either **IPv4** or **IPv6**.                          |




You could add existing virtual machines to the backend pool at this point, or you can create and add them later. You then click **Add** to add the backend pool.

![Picture 26](../media/create-backend-pool-4.png)

### Add virtual machines to the backend pool

The next task is to add the virtual machines to the existing back-end pool.

On the **Backend pools** page, select the backend pool from the list.

![Picture 27](../media/add-vm-backend-pool-1.png)

You need to enter the following information to add the virtual machine to the backend pool.

| **Field**       | **Information**                                              |
| --------------- | ------------------------------------------------------------ |
| Virtual network | Specify the name of the virtual network where the resources are located that you will be adding to the backend pool. |
| Associated to   | You need to associate the backend pool with one or more virtual machines, or to a virtual machine scale set. |
| IP Version      | Select either **IPv4** or **IPv6**.                          |




Then under the **Virtual machines** section, click **Add**.

![Picture 35](../media/add-vm-backend-pool-2.png)

Select the virtual machines you want to add to the backend pool and click **Add**.

![Picture 36](../media/add-vm-backend-pool-3.png)

Then click **Save** to add them to the backend pool.

![Picture 37](../media/add-vm-backend-pool-4.png)

![Picture 38](../media/add-vm-backend-pool-5.png)

 

### Add health probes

The next task is to create a health probe to monitor the virtual machines in the back-end pool.

On the **Backend pools** page of the load balancer, under **Settings**, select **Health probes**, and then click **Add**.

![Picture 28](../media/create-healthprobe-1.png)

You need to enter the following information on the **Add health probe** page.

| **Field**           | **Information**                                              |
| ------------------- | ------------------------------------------------------------ |
| Name                | Enter a unique name for the health probe.                    |
| Protocol            | Select either **TCP** or **HTTP**.                           |
| Port                | Specify the destination port number for the health signal. The default is port **80**. |
| Interval            | Specify the interval time in seconds between probe attempts. The default is **5** seconds. |
| Unhealthy threshold | Specify the number of consecutive probe failures that must occur before a virtual machine is considered to be in an unhealthy state. The default is **2** failures. |




You then click **Add** to add the health probe.

![Picture 29](../media/create-healthprobe-2.png)

![Picture 30](../media/create-healthprobe-3.png)

 

### Add a load balancer rule

The last task is to create a load balancing rule for the load balancer. A load balancing rule distributes incoming traffic that is sent to a selected IP address and port combination across a group of backend pool instances. Only backend instances that the health probe considers healthy receive new traffic.

On the **Health probes** page of the load balancer, under **Settings**, select **Load balancing rules**, and then click **Add**.

![Picture 32](../media/create-loadbalancing-rule-1.png)

You need to enter the following information on the **Add load balancing rule** page.

| **Field**              | **Information**                                              |
| ---------------------- | ------------------------------------------------------------ |
| Name                   | Enter a unique name for the load  balancing rule.            |
| IP Version             | Select either **IPv4** or **IPv6**.                          |
| Frontend IP address    | Select the existing public-facing IP  address of the load balancer. |
| Protocol               | Select either the **TCP** or **UDP** protocol.               |
| Port                   | Specify the port number for the load  balancing rule. The default is port **80**. |
| Backend port           | You can choose to route traffic to the  virtual machine in the backend pool using a different port than the one that  clients use by default to communicate with the load balancer (port 80). |
| Backend pool           | Select an existing backend pool.  The virtual machines in this backend pool  will be the target for the load balanced traffic of this rule. |
| Health probe           | Select an existing health probe or create  a new one.   The load balancing rule uses the health  probe to determine which virtual machines in the backend pool are healthy and  therefore can receive load balanced traffic. |
| Session persistence    | You can choose **None**, or **Client IP**, or **Client IP and protocol**.   Session persistence specifies that  traffic from a client should be handled by the same virtual machine in the  backend pool for the duration of a session. **None**  specifies that successive requests from the same client may be handled by any  virtual machine. **Client IP** specifies  that successive requests from the same client IP address will be handled by  the same virtual machine. **Client IP and protocol**  specifies that successive requests from the same client IP address and  protocol combination will be handled by the same virtual machine. |
| Idle timeout (minutes) | Specify the time to keep a TCP or HTTP  connection open without relying on clients to send *keep-alive* messages.   The default idle timeout is **4** minutes, which is also the minimum setting. The  maximum setting is 30 minutes. |
| Floating IP            | Choose between **Disabled** or **Enabled**.  With Floating IP set to **Disabled**, Azure exposes a traditional load  balancing IP address mapping scheme for ease of use (the VM instances' IP).   With Floating IP set to **Enabled**, it changes the IP address mapping to the  Frontend IP of the load balancer to allow for additional flexibility. |


You then click **Add** to add the load balancing rule.

![Picture 33](../media/create-loadbalancing-rule-2.png)

![Picture 34](../media/create-loadbalancing-rule-3.png)

 

### Test the load balancer

Having completed the various tasks to create and configure your public load balancer and its components, you should then test your configuration to ensure it works successfully. The simplest way to do this is to copy the **Public IP Address** from the public load balancer resource you created and paste it into a web browser. You should receive a response from one of the VMs in your load balancer. You could then stop whichever VM randomly responds, and once that VM has stopped, refresh the browser page to verify that you receive a response from the other VM in the load balancer instead.

 

## Quiz title: Check your knowledge 



## Multiple Choice 

What is an Availability Zone?

( ) An availability zone is a physical location that offers groups of one or more datacenters that have independent power, cooling, and networking.{{An availability zone is a unique physical location within an Azure region, offering groups of one or more datacenters that have independent power, cooling, and networking.}} 

( ) An availability zone is a logical grouping that you use to isolate virtual machine resources from each other when they're deployed.{{An availability set is a logical grouping that you use to isolate virtual machine resources from each other when they're deployed.}} 

( )  An availability zone is a logical grouping of multiple data centers which shares power and storage with other zones.{{An availability zone is a unique physical location with groups of one or more datacenters that have independent power, cooling, and networking.}}



## Multiple Choice 

You are deploying a new Azure Load Balancer that must support outbound traffic rules. Which SKU should you choose?

( ) Standard{{Standard SKU supports outbound rules through declarative outbound NAT configuration.}} 

( ) Basic{{Basic SKU does not support outbound rules.}} 

( )  Either Standard or Basic{{Basic SKU does not support outbound rules.}}