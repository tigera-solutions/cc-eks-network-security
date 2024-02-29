# Amazon EKS Security Bootcamp: Hands-on EKS workshop </br> Implementing Kubernetes Network Security for EKS Containers and Workloads

## Welcome

In this EKS-focused workshop, you will work with AWS and Calico Cloud to learn how to design and deploy best practices to secure your Kubernetes environment, detecting and blocking network-based attacks in your clusters.

Cloud-native applications require a modern approach based on the zero-trust principles of identity-based access, least privilege access, and proactively detecting threats and reducing the blast radius in case of a breach.

Calico Cloud enables fine-grained, zero-trust workload access controls between your microservices and external databases, cloud services, APIs, and other applications. It also prevents the lateral movement of threats with identity-aware segmentation that works across your workload environments, including hosts, VMs, Kubernetes components, and services.

You will come away from this workshop with an understanding of how others in your industry are securing and observing cloud-native applications in AWS, along with best practices that you can implement in your organization.

### Time Requirements

The estimated time to complete this workshop is 60-90 minutes.

### Target Audience

- Cloud Professionals
- DevSecOps Professional
- Site Reliability Engineers (SRE)
- Solutions Architects
- Anyone interested in Calico Cloud :)

### Learning Objectives

1. Review and customize security guardrails for network-based threats
2. Configure IDS/IPS, workload-centric WAF, and DDoS protection
3. Detect zero-day attacks based on suspicious container activity using syscalls, file access, and process information
4. Preview and enforce security policies to quarantine infected workloads
5. Visualize the security posture of your Kubernetes cluster

## Modules

This workshop is organized in sequential modules. One module will build up on top of the previous module, so please, follow the order as proposed below.

Module 1 - [Getting Started](modules/module-1-getting-started.md)  
Module 2 - [Deploy an EKS cluster](modules/module-2-create-eks.md)  
Module 3 - [Connect the Azure AKS cluster to Calico Cloud](modules/module-3-connect-calicocloud.md)  
Module 4 - [Security Guardrails for Network-based Threats](modules/module-4-security-guardrails.md)  
Module 5 - [Configuring IDS protection and Workload-Centric WAF](modules/module-5-ids-waf.md)  
Module 6 - [Detect Zero-Day Attacks with Threat Defence](modules/module-6-threat-defence.md)  
Module 7 - [Quarantine Infected Workloads and KSPM](modules/module-7-quarantine-kspm.md)  
Module 8 - [Clean up](modules/module-8-clean-up.md)  

---

### Useful links

- [Project Calico](https://www.tigera.io/project-calico/)
- [Calico Academy - Get Calico Certified!](https://academy.tigera.io/)
- [O’REILLY EBOOK: Kubernetes security and observability](https://www.tigera.io/lp/kubernetes-security-and-observability-ebook)
- [Calico Users - Slack](https://slack.projectcalico.org/)

**Follow us on social media**

- [LinkedIn](https://www.linkedin.com/company/tigera/)
- [Twitter](https://twitter.com/tigeraio)
- [YouTube](https://www.youtube.com/channel/UC8uN3yhpeBeerGNwDiQbcgw/)
- [Slack](https://calicousers.slack.com/)
- [Github](https://github.com/tigera-solutions/)
- [Discuss](https://discuss.projectcalico.tigera.io/)

> **Note**: The workshop provides examples and sample code as instructional content for you to consume. These examples will help you understand how to configure Calico Cloud and build a functional solution. Please note that these examples are not suitable for use in production environments.
