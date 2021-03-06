ExpressRoute is a private and resilient way to connect your on-premises networks to the Microsoft Cloud. You can access many Microsoft cloud services such as Azure and Microsoft 365 from your private data center or your corporate network. For example, you may have a branch office in San Francisco with an ExpressRoute circuit in Silicon Valley and another branch office in London with an ExpressRoute circuit in the same city. Both branch offices have high-speed connectivity to Azure resources in US West and UK South. However, the branch offices cannot connect and send data directly with one another. In other words, 10.0.1.0/24 can send data to 10.0.3.0/24 and 10.0.4.0/24 network, but NOT to 10.0.2.0/24 network.

:::image type="content" source="../media/global-reach-5558594f.png" alt-text="GlobalReach layout diagram":::


## Choose when to use ExpressRoute global reach

ExpressRoute Global Reach is designed to complement your service provider’s WAN implementation and connect your branch offices across the world. For example, if your service provider primarily operates in the United States and has linked all your branches in the U.S., but the service provider does not operate in Japan and Hong Kong SAR, with ExpressRoute Global Reach you can work with a local service provider and Microsoft will connect your branches there to the ones in the U.S. using ExpressRoute and the Microsoft global network.

:::image type="content" source="../media/global-reach-usecase-563b9539.png" alt-text="Global Reach layout with local providers for connectivity to global network":::


## Configure ExpressRoute global reach

These steps show you how to configure ExpressRoute Global Reach using Azure portal.

**Before you begin**

Before you start configuration, confirm the following criteria:

 -  You understand ExpressRoute circuit provisioning workflows.
 -  Your ExpressRoute circuits are in a provisioned state.
 -  Azure private peering is configured on your ExpressRoute circuits.
 -  If you want to run PowerShell locally, verify that the latest version of Azure PowerShell is installed on your computer.

**Identify circuits**

Identify the ExpressRoute circuits that you want use. You can enable ExpressRoute Global Reach between the private peering of any two ExpressRoute circuits, if they are in the supported countries/regions. The circuits are required to be created at different peering locations.

 -  If your subscription owns both circuits, you can choose either circuit to run the configuration in the following sections.
 -  If the two circuits are in different Azure subscriptions, you need authorization from one Azure subscription. Then you pass in the authorization key when you run the configuration command in the other Azure subscription.

:::image type="content" source="../media/expressroute-circuit-global-reach-list-46088d46.png" alt-text="Azure portal - view ExpressRoute circuits":::


**Enable connectivity**

Enable connectivity between your on-premises networks. There are separate sets of instructions for circuits that are in the same Azure subscription, and circuits that are different subscriptions.

**ExpressRoute circuits in the same Azure subscription**

1.  Select the **Azure private** peering configuration.

    :::image type="content" source="../media/expressroute-circuit-private-peering-b08fb7fd.png" alt-text="Azure portal - check that the ExpressRoute circuit is provisioned for private peering":::


2.  Select **Add Global Reach** to open the Add Global Reach configuration page.

    :::image type="content" source="../media/private-peering-enable-global-reach-1c7da165.png" alt-text="Azure portal - add circuit to GlobalReach":::


3.  On the Add Global Reach configuration page, give a name to this configuration. Select the ExpressRoute circuit you want to connect this circuit to and enter in a **/29 IPv4** for the Global Reach subnet. Azure uses IP addresses in this subnet to establish connectivity between the two ExpressRoute circuits. Do not use the addresses in this subnet in your Azure virtual networks, or in your on-premises network. Select **Add** to add the circuit to the private peering configuration.

    :::image type="content" source="../media/add-global-reach-configuration-200b331a.png" alt-text="Azure portal - Add GlobalReach details":::


4.  Select **Save** to complete the Global Reach configuration. When the operation completes, you will have connectivity between your two on-premises networks through both ExpressRoute circuits.

    :::image type="content" source="../media/save-private-peering-configuration-e0e38e8a.png" alt-text="Azure portal - save GlobalReach configuration":::


**Verify the configuration**

Verify the Global Reach configuration by selecting Private peering under the ExpressRoute circuit configuration. When configured correctly your configuration should look as followed:

:::image type="content" source="../media/verify-global-reach-configuration-664be1d8.png" alt-text="Azure portal - Verify GlobalReach configuration":::


**Disable connectivity**

To disable connectivity between an individual circuit, select the delete button next to the Global Reach name to remove connectivity between them. Then select **Save** to complete the operation.

:::image type="content" source="../media/disable-global-reach-configuration-c6a9b3d0.png" alt-text="Azure portal - disable GlobalReach configuration":::


## Quiz title: Check your knowledge

## Multiple Choice

What is ExpressRoute Global Reach primarily designed for?
( ) Connect a data center to the public internet.{{Incorrect. ExpressRoute Global Reach was not primarily designed to connect a data center to public internet.}}
( ) Connect a local service provider to a data center.{{Incorrect. ExpressRoute Global Reach was not primarily designed to connect a local service provider to a data center.}}
(x) Connect branch offices across the world.{{Correct. ExpressRoute Global Reach is designed to complement your service provider’s WAN implementation and connect your branch offices across the world.}}

## Multiple Choice

How can a network engineer for a company with offices in London and Tokyo configure communications between the two offices?
( ) Use a local service provider that has a presence in both London and Tokyo, and enable GlobalReach to connect to each local service provider location.{{Incorrect. You can use different local service providers in each location.}}
(x) Use a local service provider in London and a different local service provider in Tokyo. GlobalReach connects the branches using ExpressRoute and the Microsoft global network.{{Correct. You can use a local service provider wherever your offices are, and GlobalReach will connect the branches using ExpressRoute and the Microsoft global network.}}
( ) Use GlobalReach to connect each location to a private VPN, and use local service providers for point-to-site access.{{Incorrect. Each location should connect to GlobalNet through a local service provider.}}
