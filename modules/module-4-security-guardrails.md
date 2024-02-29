# Module 4 - Security Guardrails for Network-based Threats

Calico provides methods to enable fine-grained access controls between your microservices and external databases, cloud services, APIs, and other applications that are protected by a firewall. You can enforce controls from within the cluster using DNS egress policies from a firewall outside the cluster using the egress gateway. Controls are applied on a fine-grained, per-pod basis.

In this module, we will learn how to use Calico to create network policies to control access to and from a pod. We will install two example application stacks: The Example Voting Application and the WordPress Application. Once the applications are deployed, we will create and test network security policies with different ingress and egress rules to demonstrate how the **workload access control** is done.

1. Installing the example application stacks:

   From the cloned directory, execute:

   ```bash
   kubectl apply -f pre
   ```

Included in the `pre` there folder are two applications that will be used in the exercises during the workshop. The diagram below shows how the elements of each application communicate between themselves.

![applications](https://github.com/tigera-solutions/cc-aks-detect-block-network-attacks/assets/104035488/2564c363-7fa3-4bfe-9d11-f53fefaed957)

There are also other objects that will be created for the workshop. We will learn about them later in the workshop.

   > **Note**: Wait until all the pods are up and running to move to the next step.

## Service Graph and Flow Visualizer

Connect to Calico Cloud GUI. From the menu select `Service Graph > Default`. Explore the options.

![service_graph](https://user-images.githubusercontent.com/104035488/192303379-efb43faa-1e71-41f2-9c54-c9b7f0538b34.gif)

Connect to Calico Cloud GUI. From the menu select `Service Graph > Flow Visualizations`. Explore the options.

![flow-visualization](https://user-images.githubusercontent.com/104035488/192358472-112c832f-2fd7-4294-b8cc-fec166a9b11e.gif)

## Security Policies

Calico Security Policies provide a richer set of policy capabilities than the native Kubernetes network policies, including:  

- Policies that can be applied to any kind of endpoint: pods/containers, VMs, and/or to host interfaces
- Policies that can define rules that apply to ingress, egress, or both
- Policy rules support:
  - Actions: allow, deny, log, pass
  - Source and destination match criteria:
    - Ports: numbered, ports in a range, and Kubernetes named ports
    - Protocols: TCP, UDP, ICMP, SCTP, UDPlite, ICMPv6, protocol numbers (1-255)
    - HTTP attributes (if using Istio service mesh)
    - ICMP attributes
    - IP version (IPv4, IPv6)
    - IP or CIDR
    - Endpoint selectors (using label expression to select pods, VMs, host interfaces, and/or network sets)
    - Namespace selectors
    - Service account selectors

### The Zero Trust approach

A global default deny policy ensures that unwanted traffic (ingress and egress) is denied by default. Pods without policy (or incorrect policy) are not allowed traffic until the appropriate network policy is defined. Although the staging policy tool will help you find the incorrect or the missing policy, a global deny policy helps mitigate other lateral malicious attacks.

By default, all traffic is allowed between the pods in a cluster. Let's start by testing connectivity between application components and across application stacks. All of these tests should succeed as there are no policies in place.

We recommend creating a global default deny policy after you complete writing policy for the traffic you want to allow. Use the stage policy feature to get your allowed traffic working as expected, then lock down the cluster to block unwanted traffic.

1. Create a **staged** global default-deny policy for our workload namespaces. It will show all the traffic that would be blocked if it were enforced.

   - Go to the `Policies Board`
   - On the bottom of the tier box `default` click on `Add Policy`
     - In the `Create Policy` page enter the policy name: `default-deny`
     - On the `Applies To` session, click `Add Namespace Selector`
       First, lets apply to the `vote` and the `wordpress` namespaces
       - Select Key... `kubernetes.io/metadata.name`
       - =
       - Select Value... `vote`
       - Select ```+Add Namespace Selector``` under the ```OR```
     - On the field `Type` select both checkboxes: Ingress and Egress.
     - You are done. Click `Stage` on the top-right of your page.

   The staged policy does not affect the traffic directly but allows you to view the policy impact if it were to be enforced. You can see the denied traffic in staged policy.

2. Now, let's make use of the **Policy Recommender** feature to create the policies for the other workloads and isolate the namespaces properly.

   Let's start with the `redis` database.

   - Select the correct cluster context on the top right, then in the left hamburger menu click on ```Policies > Recommendations```

   - This takes you to the ```Policy Recommendations``` page where you need to hit the ```Enable Policy Recommendations``` (if not enabled) to spin up the Daemonset/pods for the feature.

   - Initially the page will be blank while the cluster traffic is analyzed.

   - Select ```Global Settings``` on the top right of this page and change the ```Stabilization Period``` to 5 minutes, and wait for the recommended policies to appear.

   *Stabilization Period is the learning time to capture flow logs so that a recommendation accurately reflects the cluster's traffic patterns.*

   *Processing Interval is the frequency to process new flow logs and refine recommendations.*

   - There will be two policies that show up, one per namespace of our workloads i.e the ```vote``` namespace and the ```wordpress``` namespace. Note that these are shown as ```Staged``` policies, i.e they are in a preview mode and not actually applied so that you can edit them and verify their impact before implementing.
  
   - Preview the ```vote-***``` policy by clicking the arrow:

   - Select the `vote` namespace in the Namespace dropdown:

   - Once satisfied with the rules, click on ```Actions``` on the right and click ```Add to Polocy Board```, and confirm

   - Repeat the process with the ```wordpress``` namespace policy

   - All the recommended policies are created in a special tier called `namespace-isolation`.

   - This adds the policies to the policy board in a ```Staged``` mode where you can preview the tiers and the effects of the policies before you enforce them. On the left hamburger menuy, click on ```Policies``` and ```Policies``` to go to the policy board to visualize the policies.

3. If you create all the policies correctly, at some point, you will start seeing zero traffic being denied by your default-deny staged policy. At that point, you can go ahead and enforce the default-deny policy. Voilà! The workload namespaces are now secure.

### About Tiers

Tiers are a hierarchical construct used to group policies and enforce higher precedence policies that other teams cannot circumvent, providing the basis for **Identity-aware micro-segmentation**.

All Calico and Kubernetes security policies reside in tiers. You can start “thinking in tiers” by grouping your teams and the types of policies within each group, such as security, platform, etc.

Policies are processed in sequential order from top to bottom.

![policy-processing](https://user-images.githubusercontent.com/104035488/206433417-0d186664-1514-41cc-80d2-17ed0d20a2f4.png)

Two mechanisms drive how traffic is processed across tiered policies:

- Labels and selectors
- Policy action rules

For more information about tiers, please refer to the Calico Cloud documentation [Understanding policy tiers](https://docs.calicocloud.io/get-started/tutorials/policy-tiers)

---

[:arrow_right: Module 5 - Configuring IDS protection and Workload-Centric WAF](module-5-ids-waf.md)  

[:arrow_left: Module 3 - Connect the AWS EKS cluster to Calico Cloud](module-3-connect-calicocloud.md)  
[:leftwards_arrow_with_hook: Back to Main](../README.md)  
