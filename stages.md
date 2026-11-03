# Review stages

Working file for Claude, not study material. To continue, say: **"continue from stages.md"**. Claude should read this file first, run the checks under "Resume checks", do the first stage marked NEXT, then update the marks here.

Goal: every claim in the vault is backed by a verbatim quote from an AWS page, or is explicitly flagged as unconfirmed. Evidence rule: Claude's own knowledge is never evidence. Quotes are machine-checked against the cached AWS page.

Realistic ceiling: about 9/10 on facts and 9/10 on coverage. Some facts AWS only shows in diagrams, and real exam wording can't be checked.

## Where things live

- Vault: `/mnt/c/Users/User1/notes` (edits are uncommitted unless git log says otherwise; the user runs pushes).
- Work folder (temporary): `/tmp/claude-1000/-mnt-c-Users-User1-notes/15a7515f-dcaa-4be8-9f2f-e62e7163e02a/scratchpad` (`S`).
- **Backup of the work folder:** `/home/virtual/aws-review-work/scratchpad-backup.tgz` (made 3 Nov 2026, without the page cache and snapshots). If `S` is gone, recreate it with `mkdir -p S && tar -xzf backup -C S`, then rebuild the snapshot: `git archive a8467d0 | tar -x -C S/v2`. The scripts hard-code the `S` path, so keep it.
- In `S`: `PROTOCOL.md` (first-pass rules), `COVERAGE.md`, `REVIEW.md` (second-search, adjudication and re-judging rules), `tools/` (`g`, `doc`, `toc`, `guides`, `ledgeradd`, `ledgercheck`, `covadd`, `covcheck`, `review.py`, `applyedits.py`, `progress`), `ledger/` (first-pass results), `coverage/`, `review/`, `reports/review-flags.md` (leads and warnings), `fixes/` (edits already applied).
- Agent limits: 20 at once. Use `model: sonnet` for checking agents. Each hits the 5-hour usage limit quickly, so launch in waves and save as you go.

## Resume checks (run first)

1. `git -C /mnt/c/Users/User1/notes status --short` and `git log --oneline -3`: see what is uncommitted or newly committed by the user.
2. `S/tools/progress | tail -1` and, per batch, `S/tools/ledgercheck BATCH`: which first-pass batches are incomplete.
3. `python3 S/linkcheck3.py | tail -1` should print `links 1210 bad 0`.
4. Note: the snapshot `S/v2` is commit a8467d0. Edits applied since are only in the live vault, so before any ledger-based edit, check `old` text still occurs exactly once (`tools/applyedits.py` does this and aborts otherwise).

## Stages

### Stage 1: first pass over every vault line. STATUS: DONE (3 Nov 2026)
- All batches pass `ledgercheck`: chapters, domains, guide pages, exam overview, lifecycle, index, `pe1b` to `pe5b`, `cheat`, `labs`, `refs`.
- Findings to carry into Stage 2: PE2 line 352 tag 2.1 -> 3.3 (verify in guide first); PE4 `pe4a`/`pe4b` contradicted entries (check ledger); PE5 Q64 lines 783 ("1 MB" -> 128 KB) and 789 (explanation: 50 KB objects will not transition by default); cheat lines 332 (Aurora failover), 304 (deregistration 0 to 3,600), 389 (ACM 45 days only private/imported); labs line 222 (CloudTrail delay) and Lab 7 handler lines 170-186 unchecked (API Gateway payload 2.0); PE5b Task tags and answer-key table (lines 805-830) not checked against the exam guide.
- Unsourced items go to Stage 4/5 (cheat 329, 331, 397, 253; PE5 Q31 stem; refs: EFS replication Region, Aurora 3x/5x/60% figures, Snow wording line 194, line 89).
- Weak SUPPORTED evidence noted for Stage 6: PE1 757, 769; PE4 Q20, SQS line 410; PE5 option lines 430-468, 550-553, 637-660.

### Stage 2: apply fixes from findings. STATUS: ON HOLD. The user asked not to apply any findings to the vault yet (3 Nov 2026). Do NOT edit the vault or run applyedits.py until they say so
- DONE (applied, logged in the Corrections Log under "Second review on 3 November 2026"): contradicted findings from ch01 to ch30, ch28, ch29, exam overview, service index, cheat sheet (one line), labs (three lines), Practice Exams 1 to 5 (the ones in finished batches).
- HELD (stopped at 50% usage on 3 Nov 2026, nothing from the list below is applied yet; ask the user before applying): apply the Stage 1 carry-over list (PE2 352 tag; PE4 contradicted entries from `pe4a` (3) and `pe4b` (1); PE5 Q64 lines 783 and 789; cheat 304, 332, 389 plus `cheat` earlier contradicted entry; labs 222 and Lab 7 handler check; refs log line 56). Verify each tag against the exam guide pages and each fix against its quote before `applyedits.py`; log in the Corrections Log.
- Original note: apply contradicted findings from batches finished in Stage 1 later (practice exams, cheat sheet, labs, refs). Also check ch31 and ch25 (no contradicted, only unsourced).
- Method: print `CONTRADICTED` ledger entries (`quote`, `fix`), verify the fix is supported, put them in a JSON list and run `tools/applyedits.py`. Never trust a checker's fix blindly: one proposed Task tag was wrong.

### Stage 3: finish the per-service coverage checks. STATUS: partly done
- DONE: domain items (cov-d1 to d4: no gaps), concepts and naming (cov-tech: 9 exam-process gaps), integration (cov-s2: 5 thin), databases and ML (cov-s4: 7 thin).
- NOT DONE: cov-s1 analytics, cov-s3 compute and cost, cov-s5 management, cov-s6 migration and storage, cov-s7 networking, cov-s8 security. Rerun each with `Read S/COVERAGE.md ... Your ID is: cov-sN` plus the service list (see `S/reports/` or the earlier prompts: s1 Athena, Data Exchange, Data Pipeline, EMR, Glue, Kinesis, Lake Formation, MSK, OpenSearch, Quick, Redshift, Kinesis Video Streams; s3 Budgets, CUR, Cost Explorer, Savings Plans, Batch, EC2, Auto Scaling, Beanstalk, Outposts, Serverless Application Repository, VMware Cloud on AWS, Wavelength, ECR, ECS, ECS Anywhere, EKS, EKS Anywhere, EKS Distro; s5 AWS Auto Scaling, CLI, CloudFormation, CloudTrail, CloudWatch, Compute Optimizer, Config, Control Tower, Health Dashboard, License Manager, Managed Grafana, Managed Prometheus, Console, Organizations, Proton, Service Catalog, Systems Manager, Well-Architected Tool; s6 ADS, MGN, DataSync, DMS, Snow Family, Transfer Family, Backup, EBS, EFS, FSx, S3, S3 Glacier, Storage Gateway; s7 Client VPN, CloudFront, Direct Connect, ELB, Global Accelerator, PrivateLink, Route 53, Site-to-Site VPN, Transit Gateway, VPC; s8 Artifact, ACM, CloudHSM, Cognito, Detective, Directory Service, Firewall Manager, GuardDuty, IAM Identity Center, Inspector, KMS, Macie, Network Firewall, RAM, Secrets Manager, Security Hub, Shield, WAF, IAM).
- THEN: add the thin spots and gaps found (from `coverage/*.jsonl`, entries with `st` GAP or THIN and ready-made `add` text). Known so far: SNS durability and DLQ, X-Ray sampling, Fargate isolation, Device Farm, Amplify hosting, nine exam-process facts for the exam overview (one compact addition), seven database and ML thin spots. Validate each with `covcheck`, insert after the `after` line.

### Stage 4: second search for unconfirmed claims. STATUS: not started
- About 410 claims marked UNSOURCED by the first pass. Item files are already built in `S/review/items_rs1..rs10.jsonl` (regenerate with `review.py items` after Stage 1 so they include the late batches).
- Do: launch one `sonnet` agent per group: `Read S/REVIEW.md ... stage rs (KIND rs) for GROUP rsN`. Done when `review.py check rs rsN` prints OK for all groups.

### Stage 5: adjudication. STATUS: not started
- For each UNSOURCED claim: APPLY a fix, or KEEP with evidence (distractors, absence from the in-scope list and maths are allowed bases). Rule: never delete a correct exam fact just because a source was hard to find; narrow the wording instead.
- Do: one agent per group, `stage adj (KIND adj)`, then apply every APPLY with `applyedits.py` and log it.
- Known cross-vault items still to settle: "SNS does not store" wording elsewhere (grep), WAF Classic date conflict (7 Oct 2026 vs 30 Sep 2025), Rekognition feature names (Streaming Events vs Streaming Video), DR strategy RPO/RTO figures (diagram only, keep and flag), Quick "evolved from QuickSight", Kendra and Comprehend dates.

### Stage 6: strict re-judging of "supported" entries. STATUS: not started
- About 6,100 entries marked SUPPORTED; many rest on loose quotes, especially wrong options in practice exams and self-tests. Build files with `review.py supported GROUP BATCH...`, one agent per group (`stage rj`), then adjudicate every WEAK entry as in Stage 5.

### Stage 7: final independent review. STATUS: not started
- One `opus` agent (not the one that edited) reviews every changed line (`git diff`), the Corrections Log, and a random sample of 100 SUPPORTED entries against their pages. Recount the checks: 189/189 exam guide items verbatim, 119 in-scope, 50 out-of-scope, 1,210 links, 5 exams x 65 questions, answer keys match, no duplicate stems.
- Then write the final confidence report with the remaining unconfirmed list. Update README, Home, Sources and Corrections Log dates and counts.

## Decisions made (do not redo)

- Lifecycle dates: the General Reference list gives the announcement date; product pages give "closed to new customers" dates. Both are kept and named (Simple AD, Kendra, Snowball Edge, Application Discovery Service).
- VMware Cloud on AWS stays (it is in scope) with the note that AWS no longer resells it.
- Quiz distractors whose reason is unsourced are kept if the keyed answer is sourced and the option is plainly wrong.
- Practice exams keep 20/17/15/13 of 65; the exam overview explains that scored content is 15/13/12/10 of 50.
- Study Guide and Exam Technique `[x]` boxes belong to the user: never change them.
- Memory notes: git in WSL has no GitHub credentials; the user runs pushes and merges.
