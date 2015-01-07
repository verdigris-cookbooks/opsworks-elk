opsworks-elk
============

Chef cookbook which contains Elasticsearch, Logstash, and Kibana stack for
Amazon AWS OpsWorks.


Virtual Private Cloud
=====================

Although this step is optional, VPCs are very useful in providing flexibility
and security in production applications. Since Elasticsearch have no built-in
security mechanism, setting up a VPC is highly recommended.

> Note: The instructions here assume you will be creating VPC in US West 1
(North California) region. Availability zones may differ depending on the region
you have selected.

Creating VPC
------------

1. Navigate to **VPC Dashboard** > **Your VPC**.

2. Click **Create VPC** button.

3. Enter in information as shown below:

  * **Name tag:** ELK OpsWorks
  * **CIDR block:** 10.10.0.0/16
  * **Tenancy:** Can be either *Default* or *Dedicated*

  Click **Yes, Create**.

VPC Subnet Configuration
------------------------

It is generally recommended to create subnets in different Availability Zones to
ensure failure of instances in one availability zone does not affect the normal
operation of the stack layers.

1. Navigate to **Subnets** from the sidebar and click **Create Subnet**.

2. Enter in information as shown below for the first subnet:

  * **Name tag:** ELK OpsWorks Subnet (us-west-1b)
  * **VPC:** vpc-YOUR_VPC_ID (10.10.0.0/16) | ELK
  * **Availability Zone:** us-west-1b
  * **CIDR block:** 10.10.1.0/24

  Click **Yes, Create**.

3. Enter in information as shown below for the second subnet:

  * **Name tag:** ELK OpsWorks Subnet (us-west-1c)
  * **VPC:** vpc-YOUR_VPC_ID (10.10.0.0/16) | ELK
  * **Availability Zone:** us-west-1c
  * **CIDR block:** 10.10.2.0/24

  Click **Yes, Create**.

Route Table Configuration
-------------------------

The subnets in your VPC must be associated with a route table which define how
network packets are routed in your subnets.

1. Navigate to **Route Tables** from the sidebar and click **Create Route
Table**.

2. Enter in information as shown below:

  * **Name tag:** ELK
  * **VPC:** vpc-YOUR_VPC_ID (10.10.0.0/16) | ELK

  Click **Yes, Create**.

3. Once the Route Table has been created, select the route table from the list
and click on **Subnet Associations** tab and click **Edit**.

4. Check off checkboxes in **Associate** column for both subnets and click
**Save**.

Internet Gateway Configuration
------------------------------

Internet Gateways allow instances in your VPC to be able to connect to the
Internet. Without it, your instances will not be able to receive public IP
addresses.

1. Navigate to **Internet Gateways** from the sidebar and click **Create
Internet Gateway**.

2. Enter in information as shown below:

  * **Name tag:** ELK

  Click **Yes, Create**.

3. Navigate back to **Route Tables** from the sidebar.

4. Select the route table you created in previous section.

5. Select the **Routes** tab at the bottom and click **Edit**.

6. Enter the following information on the new row:

  * **Destination:** 0.0.0.0/0
  * **Target:** igw-YOUR_GATEWAY_ID

  Click **Save**.


License
=======

This cookbook is licensed and distributed under the Simplified BSD license. See
[LICENSE](
  https://github.com/verdigris-cookbooks/opsworks-elk/blob/master/LICENSE
) for more details.
