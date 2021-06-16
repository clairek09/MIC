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