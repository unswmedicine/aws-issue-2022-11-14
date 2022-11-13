# Apparent undocumented change to AWS Cloudformation or EC2 service

Deploying [template1.yml](template1.yml) used to work but does no longer. Parameter type is not correctly set but previously worked. This is demonstrated in the way is was necessary to update the parameter type and conditional usage for the `Iops` parameters in the follows example.

Error is:

[template1.yml](template1.yml) shows the corrected version of the template, which successfully deploys.

**For both templates validation succeeeds**.

Cloudformation release history does not mention this tightening parameter types, and there is no reference to such a change in the EC2 service.

## template1

Known to work in the named account referenced in the AWS support ticket (AccountId not shown on this public resource) on 2022-11-07 and was found to no longer work 2022-11-11.


```bash
aws cloudformation validate-template --template-body file://template1.yml # succeeds
aws cloudformation deploy --template-file template1.yml --stack-name test-template1-yml-delete-me
aws cloudformation describe-stack-events --stack-name test-template1-yml-delete-me > stack-events-test-template1-yml-delete-me.json
```

**Cloudformation does not successfully create the resource** as seen at [stack-events-test-template2-yml-delete-me.json](stack-events-test-template2-yml-delete-me.json)

## template2

```bash
aws cloudformation validate-template --template-body file://template2.yml # succeeds
aws cloudformation deploy --template-file template2.yml --stack-name test-template2-yml-delete-me
aws cloudformation describe-stack-events --stack-name test-template2-yml-delete-me > stack-events-test-template2-yml-delete-me.json
```

Cloudformation **successfully** creates the resource as seen at [stack-events-test-template2-yml-delete-me.json](stack-events-test-template2-yml-delete-me.json)