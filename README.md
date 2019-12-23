# Create F5 BIG-IP VM or General VM
This module is supporting to create F5 BIG-IP VM with landingzone_vdc_demo( https://www.arnaudlheureux.io/2019/11/15/cloud-adoption-framework-landing-zones-with-terraform/ )which is more developped compared to the previous version blueprints_tranquility(https://github.com/aztfmod/blueprints/tree/master/blueprint_tranquility).<br>
This is working as one of its module and also you can use this for your own standalone VM creator after some modify.
You can check the previous version detail from README_v0.md file.

## Getting Started
You need to update VM and plan part of the variable.tf file for your environment.<br/>
and add some inforamtion(your own information) to end of the foundations.tf file under landingzone_vdc_demo root diretory.
You can use all of the defaults parameters for your testing after some files updating like blueprint.tf, output.tf under each blueprint_networking directories where you want to add BIG-IP with main module file for F5BIG-IP.

If you want to add BIG-IP into blueprint_networking_shared_egress and blueprint_networking_shared_transit, you need to edit 2 files(blueprint.tf, output.tf) in the each directory and add F5BIGIP_Egress.tf, F5BIGIP_Transit.tf.
Of course, you can use your won module name not use them(F5BIGIP_Egress.tf, F5BIGIP_Transit.tf).

So, let's see example lines for each file.
# blueprint_networking


  
# F5 module in foundations.tf
#Create F5 BIGIP VE<br>
module "f5_bigip" {<br>
 source  = "git@github.com:jungcheolkwon/f5bigip.git?ref=v1.75"<br>

 resource_group_name       = module.resource_group_hub.names["HUBTRANSITNET"]<br>
 location                  = var.location_map["region1"]<br>
 tags                      = var.tags_hub<br>
 virtual_network_name      = module.virtual_network["vnet_name"]<br>
 subnet_id                 = module.virtual_network.vnet_subnets["Intranet"]<br>
 network_security_group_id = module.virtual_network.nsg_vnet["Intranet"]<br>
}<br>
![example](https://github.com/jungcheolkwon/f5-bigip/blob/master/foundations.tf.png)

