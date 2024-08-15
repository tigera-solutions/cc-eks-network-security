# Module 7 - Quarantine a Workload and KSPM

## Quarantine a Workload

Suppose you have a compromised workload in your environment and want to conduct further investigation on it. In that case, you should not terminate the workload but isolate it, so it will not be able to cause damage or spread laterally across your environment. In this situation, you should quarantine the pod by applying a security policy to it that will deny all the egress and ingress traffic and log all the communications attempts from and to that pod.

We have the `quarantine` policy created in the `security` tier. This policy has a label selector of `quarantine = true`. Let's see how it works.

1. Execute the following commands from the attacker pod (if you did quit from its shell, it got deleted. Create it again if it's the case.).

   - Test the connection to a local service

     ```bash
     curl -Ism2 http://vote.vote
     ```

   - Test the connectivity with the Kubernetes API

     ```bash
     curl -Ism2 -k https://kubernetes:443/versions
     ```  

   - Test the connectivity with the internet

     ```bash
     curl -Ism2 http://neverssl.com
     ```  

2. Label the attacker pod with `quarantine = true`.

   ```bash
   kubectl label pod attacker quarantine=true
   ```

3. Repeat the tests from step 1. Now, as you can see, the cannot establish communication with any of the destinations.

---

## Visualize security posture of your Kubernetes cluster

### Timeline

What changed, who did it, and when? This information is critical for security. Native Kubernetes doesn’t provide an easy way to capture audit logs for pods, namespaces, service accounts, network policies, and endpoints. The Calico Cloud timeline provides audit logs for all changes to network policy and other resources associated with your Calico Cloud deployment.

1. On the Calico Cloud GUI, navigate to `Activity` and explore the entries in the `Timeline`.

![timeline](https://github.com/tigera-solutions/cc-aks-detect-block-network-attacks/assets/104035488/27bfeaff-4c1a-4d3d-b5c4-5234ecb13a52)

**Congratulations! You completed this workshop!**

---

[:arrow_right: Module 8 - Clean up](module-8-clean-up.md)  

[:arrow_left: Module 6 - Realtime Container Thread Defence](module-6-threat-defence.md)  
[:leftwards_arrow_with_hook: Back to Main](../README.md)  
