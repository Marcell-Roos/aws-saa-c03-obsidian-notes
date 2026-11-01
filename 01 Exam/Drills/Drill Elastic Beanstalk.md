---
tags: [drill, scope/in]
---

# Drill Elastic Beanstalk

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Developers want to deploy code quickly without managing infrastructure but must retain full control of the underlying resources"* → **[[AWS Elastic Beanstalk|Elastic Beanstalk]]** (that's its identity phrase verbatim)
- *"Deploy new version as fast as possible; brief downtime is acceptable (dev environment)"* → **All at once** (speed + downtime-OK = the only reason to pick it)
- *"Deploy with no downtime and no additional cost"* → **Rolling** (batches reuse existing instances, capacity dips but nothing new is billed)
- *"Deploy with no downtime while maintaining full capacity"* → **Rolling with additional batch** (the extra batch covers the gap)
- *"Deployment must be safest possible with quick rollback if health checks fail"* → **Immutable** (bad deploy? delete the new fleet, old one untouched)
- *"Test the new version against a separate URL, then switch all traffic instantly with instant rollback"* → **Blue/Green with CNAME swap** ([[DNS Fundamentals|DNS]] swap both ways)
- *"Beanstalk app's database was lost when the environment was terminated — prevent this in production"* → **Create [[Amazon RDS|RDS]] outside the environment; connect via environment variables** ([[Loose Coupling|decouple]] lifecycles)
- *"Migrate a database out of an existing Beanstalk environment"* → **Snapshot the RDS instance → restore as standalone RDS** (then reconnect via env vars)
- *"Long-running background jobs from a queue alongside a Beanstalk web app"* → **Worker environment** (the SQS-consuming tier)
- *"Customize packages and configuration of Beanstalk instances at deploy time"* → **.ebextensions** (config files in the source bundle)

## Pocket card

| Keyword | Answer |
|---|---|
| "Quickly deploy, no infra mgmt, KEEP control" | Elastic Beanstalk |
| Fastest deploy, downtime OK | All at once |
| No downtime, no extra cost | Rolling |
| No downtime, full capacity | Rolling + additional batch |
| Safest rollback (delete new fleet) | Immutable |
| DNS CNAME swap, instant rollback | Blue/Green |
| DB died with environment | Create RDS OUTSIDE env (env vars) |
| Move DB out of env | Snapshot → standalone RDS |
| SQS-driven background tier | Worker environment |
| Instance/env customization files | .ebextensions |
| Beanstalk pricing | Free — pay for resources only |
| Fine-grained IaC instead | [[AWS CloudFormation\|CloudFormation]] |

---
**Up:** [[Drills Map]]
