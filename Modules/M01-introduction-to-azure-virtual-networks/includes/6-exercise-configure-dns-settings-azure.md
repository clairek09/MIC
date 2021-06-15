In this unit, you will configure DNS name resolution for Contoso Ltd. You will create a private DNS zone named contoso.com, link the VNets for registration and resolution, and then create two virtual machines and test the configuration.

##Create a private DNS Zone

1.	Go to Azure Portal.
1.	On the Azure home page, in the search bar, type dns, and then select **Private DNS zones.**

![Create-private-DNS-zone](../media/Create-private-DNS-zone.png)

1.	In Private DNS zones, select **+ Create.**
1.	Use the information in the following table to create the private DNS zone.

|Tab|Option|Value|
|---|---|---|
|Basics|Resrouce Group |ContosoResourceGroup|
||Name |Contoso.com|
|Tags|No changes required |
|Review + create|Review your settings and select Create |

1.	Wait until the deployment is complete, and then select **Go to resource.**
1.	Verify that the zone has been created.
