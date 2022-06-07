# load balancer limits - Rules per NIC (across all IPs on a NIC)	300
https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer

<img src="/limit.png" width="90%">

This limit means for your NICs in the backend pool, one NIC can only has 300 rules programed.
This 300 rules will be shared across outbound, load balancing, and NAT rules.

## Lab to check
Let's look into more detail with the lab configuration to help you understand this behavior.
Now we have a load balancer lb_japan_Standard created with 2 backend pool and 3 public IPs.



For the backend pool1, it already has 300 rules got installed.
 
<img src="/pool1.png" width="90%">

So in this case, you will not be able to install any new rule ( outbound, load balancing, and NAT) with this backend pool pool1.
You will received an error message when you try to create a new rule with pool1.

### Load balancing rule

<img src="/loadbalanceruleerror.png" width="90%">

### NAT rule

<img src="/NATruleerror.png" width="90%">

### Outbound rule

<img src="/Outboundruleerror.png" width="90%">


If you would like to have more then 300 rules per NIC, you need to add a new pool and then you will have new VMs in that pool which can support more 300 new rule for that pool.

<img src="/pool1andpool2.png" width="90%">

And if we look at the public IP level, you can have 1 public IP which has more then 300 rules  associated. So add new public IP won't help you to increase the total rules which can be installed. 

<img src="/publicip.png" width="90%">
