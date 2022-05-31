# NAT gateway 

A NAT Gateway allows ECS instances deployed in a VPC to access the
Internet without being accessible from the Internet. SNAT is used to
fulfill this role.

A NAT Gateway also allows ECS instances deployed in a VPC to be accessed
from the Internet by associating EIPs with ECS instances. This role is
performed by the DNAT.

NAT Gateways use the Anti -DDoS service to secure these accesses.

## The concepts of DNAT and SNAT 

DNAT (Destination Network Address Translation) is used to redirect
incoming packets whose destination is a public address or port to a
private IP address or port within the network.

SNAT (Source Network Address Translation) is executed after the routing
decision while DNAT is executed before the routing decision.

SNAT is used to access the Internet from the Cloud network.

DNAT is used, for example, to make a website hosted in the Cloud network
accessible from the Internet.

## Management of a NAT gateway 

To create a NAT Gateway instance:
-   Go to the `NAT Gateway` console,
-   Click on `Create NAT Gateway`,
-   `Region and Zone`: this is the region,

The region must be the same as that of the VPC instance.
-   `Zone`: this is the zone where to deploy the instance,`
-   VPC ID`: this is the VPC in which the NAT Gateway is created; the
    VPC cannot be changed later,
-   `VSwitch ID`: this is the vSwitch to which the NAT Gateway is
    attached,`
-   Gateway Type`: this is the type of NAT Gateway (`Enhanced` or
    `Standard`),`
-   Billing Method`: this is`` the billing method,`
-   Billing Cycle`: this is the billing cycle of the NAT Gateway
    instance.
-   Click on `Activate Now`,
-   Click on `Buy Now`.

![Une image contenant texte Description générée
automatiquement](./media/image210.png){width="4.5in"
height="3.5055555555555555in"}

A VPC can only have one NAT Gateway.

VPCs with a destination CIDR block `0.0.0.0/0` do`` not appear in
the list.

To modify a NAT Gateway instance:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on `Manage` on the line of the instance to be modified,
-   Change the name and description,
-   Click on `OK`.

To delete a NAT Gateway instance:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on `... | Delete` on the line of the instance to be
    deleted,
-   Click on `OK`.

## Management of a DNAT table 

DNAT allows to map a public IP address of a VPC ECS instance to a
private IP address of the VPC. The public IP address is then used to
provide access from the Internet.

A NAT Gateway instance includes a DNAT table, each entry of which
includes:
-   a public IP address,
-   a public port,
-   a private IP address,
-   a private port,
-   a protocol.

The data packets received from the public IP address are then forwarded
to the ECS instance according to the mapping rules.

DNAT supports port mapping and IP address mapping.

With port mapping, the NAT Gateway forwards requests for the specified
protocol and port to the selected ECS instance on the specified port.

With IP address mapping, the NAT Gateway forwards requests for the
specified IP address to the selected ECS instances. Requests to the
public IP address are forwarded to the corresponding ECS instance.

To add a DNAT entry:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click `Configure DNAT` on the line of the instance,
-   Click `Create DNAT Entry`,
-   `Select Public IP Address`: this is the public IP address,
-   `Select Private IP Address`: this is the private IP address of the
    ECS instance,

It can be specified manually (it must be part of the VPC private IP
address set) or automatically (by selecting an ECS instance of the VPC).
-   `Port Settings`: this is the mapping method:

```{=html}
<!-- -->
```
-   `Any Port`: this is the method for mapping IP addresses,

The ECS instance receives requests from all ports and protocols.
-   `Specific Port`: this`` is the method of mapping ports,

The NAT Gateway instance forwards requests for the specified port and
protocol to the specified ECS instance on the specified port.
-   `Entry Name`: this is`` the name of the entry,
-   Click on `Confirm`.

![Une image contenant texte Description générée
automatiquement](./media/image211.png){width="4.5in"
height="3.672222222222222in"}

To edit a DNAT entry:
-   Go to the `NAT Gateway` console,
-   Select a region,
-   Click `Configure DNAT` on the line of the instance,
-   Click on `Edit` on the line of the entry,
-   Modify the entry,
-   Click on `Confirm`.

To delete a DNAT entry:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click `Configure DNAT` on the line of the instance,
-   Click on `Delete` on the line of the entry,
-   Click on `OK`.

## Management of a SNAT table 

SNAT is an Internet proxy service for ECS instances of type VPC. The ECS
instances can then access the Internet.

A NAT Gateway has a SNAT table. Each entry includes:
-   a vSwitch: this is where the ECS instance is located,
-   a public IP address: this is the EIP linked to the NAT Gateway.

When an ECS instance of the specified vSwitch sends an Internet access
request, the ECS instance uses the public IP address of the NAT Gateway
instance to access the Internet. This is the default behavior of ECS
instances.

To add a SNAT entry:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click `Configure SNAT Gateway` on the line of the instance,
-   Click on `Create SNAT Entry`,
-   If` Specify vSwitch` is selected, the ECS instances attached to
    the vSwitch use the EIP to access the Internet:`

```{=html}
<!-- -->
```
-   Select vSwitch`: this is the vSwitch,
-   `vSwitch CIDR Block:` this is the CIDR block of the selected
    vSwitch,

```{=html}
<!-- -->
```
-   If` Specify ECS`, the ECS instances use the EIP to access the
    Internet:`

```{=html}
<!-- -->
```
-   Select ECS Instance`: these are the ECS instances,
-   `ECS CIDR Block`: this is the CIDR block of the selected ECS
    instance,

```{=html}
<!-- -->
```
-   `Select Public IP Address`: this is the public IP address used to
    access the Internet:

```{=html}
<!-- -->
```
-   `Use One IP Address`: this is the EIP used,
-   `Use Multiple IP Addresses`: these are the EIPs used (they must
    all have the same bandwidth plan),

```{=html}
<!-- -->
```
-   `Entry Name`: this is the name of the entry,
-   Click on `Confirm`.

![Une image contenant texte Description générée
automatiquement](./media/image212.png){width="4.5in"
height="3.577777777777778in"}

To edit a SNAT entry:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on `Configure SNAT` on the line of the instance,
-   Click on `Edit` on the line of the entry,
-   Modify the entry,
-   Click on `Confirm`.

To delete a SNAT entry:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on `Configure SNAT` on the line of the instance,
-   Click on `Remove` on the line of the entry,
-   Click on `OK`.

## Association and disassociation of an EIP with a NAT Gateway 

A NAT Gateway instance must have an associated EIP.

To associate an EIP:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on `Associate Now` on the line of the instance,`
-   Public IP`: this is the EIP to be associated,
-   Click on OK.

![Une image contenant texte Description générée
automatiquement](./media/image213.png){width="2.113487532808399in"
height="0.7044958442694663in"}

To disassociate an EIP:
-   Go to the `NAT Gateway` console,
-   Select the region,
-   Click on the instance ID,
-   Click on `Dissociate` on the line of the instance,
-   Click `OK`.

## Protection of a NAT Gateway with Anti-DDoS 

Alibaba Cloud provides Anti-DDoS protection for NAT Gateway instances.
The principle is the same as for SLB instances.

The thresholds are calculated as follows:

  -----------------------------------------------------------------------
  EIP bandwidth     Scrubbing         Scrubbing         Default
                    threshold for     threshold for     blackholing
                    maximum traffic   maximum traffic   threshold
                    (bits/s)          (packets/s)       
  ----------------- ----------------- ----------------- -----------------
  <= 800 Mbps      800 Mbps          120,000           1.5 Gbps

  > 800 Mbps       Configured        Configured        Configured
                    bandwidth         bandwidth x 150   bandwidth x 2
  -----------------------------------------------------------------------

