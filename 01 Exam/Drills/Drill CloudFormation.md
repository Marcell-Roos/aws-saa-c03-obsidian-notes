---
tags: [drill, scope/in]
---

# Drill CloudFormation

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Team must review what changes a template update will make before applying it"* → **Change Sets** (preview = change set, always)
- *"Deploy standardized security/compliance resources to all accounts in an organization, across regions"* → **[[AWS CloudFormation|CloudFormation]] StackSets** (one template → many accounts/regions)
- *"Ensure the [[Amazon RDS|RDS]] database is not deleted when the stack is torn down"* → **DeletionPolicy: Retain** (or Snapshot if they want a final copy)
- *"Determine whether anyone modified stack resources manually via the console"* → **Drift Detection** (template vs. reality diff)
- *"Deploy identical environments repeatedly across regions with no manual steps"* → **CloudFormation templates** (the core IaC pitch)
- *"Prevent accidental updates to a critical resource during stack updates"* → **Stack Policy** (update-protection inside a stack)
- *"Reuse a common [[Amazon VPC|VPC]] pattern across many templates"* → **Nested Stacks** (componentize the recipe)

## Pocket card

| Keyword | Answer |
|---|---|
| Preview changes before update | Change Sets |
| Many accounts + regions, one template | StackSets |
| Keep data on stack delete | DeletionPolicy Retain / Snapshot |
| Detect manual console edits | Drift Detection |
| Protect resource during updates | Stack Policy |
| Reusable template components | Nested Stacks |
| Share values between stacks | Outputs + Export / ImportValue |
| Only required template section | Resources |
| Failed creation | Automatic rollback (default) |

---
**Up:** [[Drills Map]]
