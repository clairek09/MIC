Exercise - Design and implement IP addressing for Azure virtual networks

Now you're ready to create and deploy some virtual networks with the IP addresses that you planned.

Consider the fictional organization Contoso Ltd, which is in the process of migrating infrastructure and applications to Azure. In your role as network engineer, you must  plan and implement three virtual networks and subnets to support resources in those virtual networks.

The CoreServicesVnet virtual network is deployed in the US West region. This virtual network will have the largest number of resources. It will have connectivity to on-premises networks through a VPN connection. This network will have web services, databases, and other systems that are key to the operations of the business. Shared services, such as domain controllers and DNS also will be located here. A large amount of growth is anticipated, so a large address space is necessary for this virtual network.

The ManufacturingVnet virtual network is deployed in the North Europe region, near the location of your organization's manufacturing facilities. This virtual network will contain systems for the operations of the manufacturing facilities. The organization is anticipating a large number of internal connected devices for their systems to retrieve data from, such as temperature, and will need an IP address space that it can expand into.

The ResearchVnet virtual network is deployed in the West India region, near the location of the organization's research and development team. The research and development team uses this virtual network. The team has a small, stable set of resources that is not expected to grow. The team needs a small number of IP addresses for a few virtual machines for their work.

![Network layout for Contoso. 
On-premises 10.10.0.0/16
ResearchVNet West India 10.40.40.0/24
CoreServicesVNet West US 10.20.0.0/16
ManufacturingVNet North Europe 10.30.0.0/16
](../media/design-implement-vnet-peering.png)


You will create the following resources:

:::row:::
:::column:::

Virtual Network

:::column-end:::
:::column:::

Region

:::column-end:::
:::column:::

Virtual network address space

:::column-end:::
:::column:::

Subnet

:::column-end:::
:::column:::

Subnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

CoreServicesVnet

:::column-end:::
:::column:::

West US

:::column-end:::
:::column:::

10.20.0.0/16

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

GatewaySubnet

:::column-end:::
:::column:::

10.20.0.0/27

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

SharedServicesSubnet

:::column-end:::
:::column:::

10.20.10.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

DatabaseSubnet

:::column-end:::
:::column:::

10.20.20.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

PublicWebServiceSubnet

:::column-end:::
:::column:::

10.20.30.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

ManufacturingVnet

:::column-end:::
:::column:::

North Europe

:::column-end:::
:::column:::

10.30.0.0/16

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

ManufacturingSystemSubnet

:::column-end:::
:::column:::

10.30.10.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

SensorSubnet1

:::column-end:::
:::column:::

10.30.20.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

SensorSubnet2

:::column-end:::
:::column:::

10.30.21.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

SensorSubnet3

:::column-end:::
:::column:::

10.30.22.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

ResearchVnet

:::column-end:::
:::column:::

West India

:::column-end:::
:::column:::

10.40.40.0/24

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

ResearchSystemSubnet

:::column-end:::
:::column:::

10.40.40.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

These virtual networks and subnets are structured in a way that accommodates existing resources yet allows for projected growth. Let's create these virtual networks and subnets to lay the foundation for our networking infrastructure.

Create the Contoso resource group

Go to [Azure Portal](https://portal.azure.com/).

On the home page, under Azure services, select Resource groups. ![Azure portal home page with Resource groups highlighted.](../media/azure-portal-home-page-annotated.png) 

 In Resource groups, select + Create.

Use the information in the following table to create the resource group.

:::row:::
:::column:::

Tab

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

Basics

:::column-end:::
:::column:::

Resource group

:::column-end:::
:::column:::

ContosoResourceGroup

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Region

:::column-end:::
:::column:::

(US) West US

:::column-end:::
:::row-end:::
:::row:::
:::column:::

Tags
:::column-end:::
:::column span="2":::

No changes required
:::column-end:::
:::row-end:::
:::row:::
:::column:::

Review + create
:::column-end:::
:::column span="2":::

Review your settings and select Create
:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

In Resource groups, verify that ContosoResourceGroup appears in the list.

Create the CoreServicesVnet virtual network and subnets

On the Azure Portal home page, select Create a resource.

In Search services and marketplace, enter virtual network. ![Azure Portal Create a resource page with Search services and marketplace box highlighted.](../media/create-resource-search-virtual-network-annotated.png) 

In Marketplace, in Virtual Network, select Create > Virtual network. ![Virtual Network tile with Create Virtual network highlighted.](../media/virtual-network-service-annotated.png) 

Use the information in the following table to create the CoreServicesVnet virtual network.Remove or overwrite the default IP Address space

![IP address configuration in Azure portal ](../media/ip-addresses-configuration.png)

:::row:::
:::column:::

Tab

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

Basics

:::column-end:::
:::column:::

Resource Group

:::column-end:::
:::column:::

ContosoResourceGroup

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Name

:::column-end:::
:::column:::

CoreServicesVnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Region

:::column-end:::
:::column:::

(US) West US

:::column-end:::
:::row-end:::
:::row:::
:::column:::

IP Addresses

:::column-end:::
:::column:::

IPv4 address space

:::column-end:::
:::column:::

10.20.0.0/16

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

Use the information in the following table to create the CoreServicesVnet subnets.

To begin creating each subnet, select + Add subnet. To finish creating each subnet, select Add.

:::row:::
:::column:::

Subnet

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

GatewaySubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

GatewaySubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.20.0.0/27

:::column-end:::
:::row-end:::
:::row:::
:::column:::

SharedServicesSubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

SharedServicesSubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.20.10.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

DatabaseSubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

DatabaseSubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.20.20.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

PublicWebServiceSubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

PublicWebServiceSubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.20.30.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

To finish creating the CoreServicesVnet and its associated subnets, select Review + create.

Verify your configuration passed validation, and then select Create.

Create the ManufacturingVnet virtual network and subnets

On the Azure Portal home page, select Create a resource.

In Search services and marketplace, enter virtual network. ![Azure Portal Create a resource page with Search services and marketplace box highlighted.](../media/create-resource-search-virtual-network-annotated.png) 

In Marketplace, in Virtual Network, select Create > Virtual network. ![Virtual Network tile with Create Virtual network highlighted.](../media/virtual-network-service-annotated.png) 

Use the information in the following table to create the ManufacturingVnet virtual network.

:::row:::
:::column:::

Tab

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

Basics

:::column-end:::
:::column:::

Resource Group

:::column-end:::
:::column:::

ContosoResourceGroup

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Name

:::column-end:::
:::column:::

ManufacturingVnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Region

:::column-end:::
:::column:::

(Europe) North Europe

:::column-end:::
:::row-end:::
:::row:::
:::column:::

IP Addresses

:::column-end:::
:::column:::

IPv4 address space

:::column-end:::
:::column:::

10.30.0.0/16

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

Use the information in the following table to create the ManufacturingVnet subnets.

To begin creating each subnet, select + Add subnet. To finish creating each subnet, select Add.

:::row:::
:::column:::

Subnet

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

ManufacturingSystemSubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

ManufacturingSystemSubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.30.10.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

SensorSubnet1

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

SensorSubnet1

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.30.20.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

SensorSubnet2

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

SensorSubnet2

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.30.21.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

SensorSubnet3

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

SensorSubnet3

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.30.22.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

To finish creating the ManufacturingVnet and its associated subnets, select Review + create.

Verify your configuration passed validation, and then select Create.

Create the ResearchVnet virtual network and subnets

On the Azure Portal home page, select Create a resource.

In Search services and marketplace, enter virtual network. ![Azure Portal Create a resource page with Search services and marketplace box highlighted.](../media/create-resource-search-virtual-network-annotated.png) 

In Marketplace, in Virtual Network, select Create > Virtual network. ![Virtual Network tile with Create Virtual network highlighted.](../media/virtual-network-service-annotated.png) 

Use the information in the following table to create the ResearchVnet virtual network.

:::row:::
:::column:::

Tab

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

Basics

:::column-end:::
:::column:::

Resource Group

:::column-end:::
:::column:::

ContosoResourceGroup

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Name

:::column-end:::
:::column:::

ResearchVnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Region

:::column-end:::
:::column:::

(Asia Pacific) West India

:::column-end:::
:::row-end:::
:::row:::
:::column:::

IP Addresses

:::column-end:::
:::column:::

IPv4 address space

:::column-end:::
:::column:::

10.40.40.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

Use the information in the following table to create the ResearchVnet subnet.

To begin creating the subnet, select + Add subnet. To finish creating the subnet, select Add.

:::row:::
:::column:::

Subnet

:::column-end:::
:::column:::

Option

:::column-end:::
:::column:::

Value

:::column-end:::
:::row-end:::
:::row:::
:::column:::

ResearchSystemSubnet

:::column-end:::
:::column:::

Subnet name

:::column-end:::
:::column:::

ResearchSystemSubnet

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

Subnet address range

:::column-end:::
:::column:::

10.40.40.0/24

:::column-end:::
:::row-end:::
:::row:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::column:::

:::column-end:::
:::row-end:::

To finish creating the ResearchVnet and its associated subnet, select Review + create.

Verify your configuration passed validation, and then select Create.

Verify the creation of VNets and Subnets

On the Azure Portal home page, select All resources.

![Azure portal home page with All resources highlighted.](../media/azure-portal-home-page-all-resources-annotated.png)


Verify that the CoreServicesVnet, ManufacturingVnet, and ResearchVnet are listed. Your list should look like this:

![All resources list with CoreServicesVnet, ManufacturingVnet, and ResearchVnet highlighted.](../media/all-resources-list-annotated.png)


Note that Azure creates NetworkWatchers for each region that you use.

Select CoreServicesVnet.

In CoreServicesVnet, under Settings, select Subnets.

In CoreServicesVnet | Subnets, verify that the subnets you created are listed, and that the IP address ranges are correct.

![List of subnets in CoreServicesVnet.](../media/verify-subnets-annotated.png)


Repeat steps 4 -6 for each subnet.

Congratulations! You have successfully created a resource group, three VNets, and their associated subnets.






|Tab|Option|Value|
|---|---|---|
|Basics|Resrouce Group |ContosoResourceGroup|
||Name |ManufacturingVnet|
||Region |(Europe) North Europe|
|IP Addresses|IPv4 Address space |10.30.0.0/16|