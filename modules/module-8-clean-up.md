# Module 8 - Clean up

1. Delete the example application stacks.

   ```bash
   kubectl delete -f pre/004-web-app-manifest.yaml
   kubectl delete -f pre/005-vote-app-manifest.yaml
   ```

2. Delete the EKS cluster.

   ```bash
   eks delete cluster \
     --name $CLUSTERNAME
     --region $REGION
   ```

3. Delete environment variables backup file.

   ```bash
   rm ~/labVars.env
   ```

---

[:arrow_left: Module 7 - Quarantine Infected Workloads and KSPM](module-7-quarantine-kspm.md)  

[:leftwards_arrow_with_hook: Back to Main](../README.md)
