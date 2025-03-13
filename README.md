# CLOUD-SECURITY-WITH-AWS-IAM
A practical guide to securing AWS using IAM. 
# aws iam policy for ec2 instance control  

## overview  
this repository contains an aws iam policy that grants users permission to start, stop, and describe ec2 instances **only** if they are tagged with `env=development`. it also explicitly denies the ability to create or delete tags for **any** ec2 instance to maintain security and prevent privilege escalation.  

## policy details  
### ✅ **allowed actions (only for `env=development` instances)**  
- start ec2 instances  
- stop ec2 instances  
- describe ec2 instances  

### ❌ **denied actions (for all instances)**  
- creating new tags  
- deleting existing tags  

## iam policy  

```json
{
    "version": "2012-10-17",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "ec2:startinstances",
                "ec2:stopinstances",
                "ec2:describeinstances"
            ],
            "resource": "*",
            "condition": {
                "stringequals": {
                    "ec2:resourcetag/env": "development"
                }
            }
        },
        {
            "effect": "deny",
            "action": [
                "ec2:createtags",
                "ec2:deletetags"
            ],
            "resource": "*"
        }
    ]
}
