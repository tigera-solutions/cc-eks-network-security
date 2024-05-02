# Module 8 - Clean up

1. Delete the example application stacks.

   ```bash
   kubectl delete -f pre/004-web-app-manifest.yaml
   kubectl delete -f pre/005-vote-app-manifest.yaml
   ```

2. Delete the EKS cluster.

   ```bash
   eksctl delete cluster \
     --name $CLUSTERNAME
     --region $REGION
   ```

3. Delete environment variables backup file.

   ```bash
   rm ~/labVars.env
   ```

4. Clean up IAM resources

   ```bash
   # use user that has access to delete IAM resources
   export AWS_ACCESS_KEY_ID='<your_accesskey_id>'
   export AWS_SECRET_ACCESS_KEY='<your_secretkey>'

   # delete IAM resources
   IAM_ROLE='tigera-workshop-admin'
   ADMIN_POLICY_ARN=$(aws iam list-policies --query 'Policies[?PolicyName==`AdministratorAccess`].Arn' --output text)

   aws iam remove-role-from-instance-profile --role-name $IAM_ROLE --instance-profile-name $IAM_ROLE
   aws iam detach-role-policy --role-name $IAM_ROLE --policy-arn $ADMIN_POLICY_ARN
   aws iam delete-role --role-name $IAM_ROLE
   aws iam delete-instance-profile --instance-profile-name $IAM_ROLE
   ```

---

[:arrow_left: Module 7 - Quarantine Infected Workloads and KSPM](module-7-quarantine-kspm.md)  

[:leftwards_arrow_with_hook: Back to Main](../README.md)
