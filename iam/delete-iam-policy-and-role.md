# You need the ChangeThis >>>ChangeToYourselfPolicyPreifx<<< as yourself policyName
```bash
aws iam list-policies > policies.json
cat policies.json | jq '.Policies[]|select (.PolicyName| startswith("ChangeToYourselfPolicyPreifx"))'|jq .Arn|sed 's/\"//g' > delete_policy
while read policy;do aws iam detach-role-policy --role-name `aws iam list-entities-for-policy --policy-arn $policy|jq .PolicyRoles[].RoleName|sed 's/\"//g'` --policy-arn $policy && echo detach $policy;done < delete_policy
while read policy;do aws iam delete-policy --policy-arn $policy && echo delete $policy; done < delete_policy
```

# You need the ChangeThis >>>ChangeToYourselfRolePreifx<<< as yourself RoleName
```bash
aws iam list-roles > roles.json
cat roles.json | jq '.Roles[] | select(.RoleName | startswith("ChangeToYourselfRolePreifx"))'|jq .RoleName|sed 's/\"//g'  > delete_role
while read role; do     aws iam delete-role --role-name $role && echo delete $role; done < delete_role
```
