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

### Stage 2: apply fixes from findings. STATUS: DONE (3 Nov 2026, user committed earlier work and released the hold). Applied: PE5 Q64 (783, 789), PE4 Athena line, cheat Aurora and ACM lines (fixes/g12.json). Already applied before: cheat 304, PE3 Firehose, PE4 tag and stem, labs three lines. Checked, left unchanged: PE2 Q28 stays 2.1 (guide lists caching under 2.1 and 3.3), PE4 load balancer stays 4.2. Remaining: PE5b Task tags and key table (lines 805-830) vs the guide; Lab 7 handler (API Gateway payload 2.0). UNSOURCED fixes (labs 222, cheat 253/329/331/397, PE5, refs) belong to Stages 4-5
- DONE (applied, logged in the Corrections Log under "Second review on 3 November 2026"): contradicted findings from ch01 to ch30, ch28, ch29, exam overview, service index, cheat sheet (one line), labs (three lines), Practice Exams 1 to 5 (the ones in finished batches).
- HELD (stopped at 50% usage on 3 Nov 2026, nothing from the list below is applied yet; ask the user before applying): apply the Stage 1 carry-over list (PE2 352 tag; PE4 contradicted entries from `pe4a` (3) and `pe4b` (1); PE5 Q64 lines 783 and 789; cheat 304, 332, 389 plus `cheat` earlier contradicted entry; labs 222 and Lab 7 handler check; refs log line 56). Verify each tag against the exam guide pages and each fix against its quote before `applyedits.py`; log in the Corrections Log.
- Original note: apply contradicted findings from batches finished in Stage 1 later (practice exams, cheat sheet, labs, refs). Also check ch31 and ch25 (no contradicted, only unsourced).
- Method: print `CONTRADICTED` ledger entries (`quote`, `fix`), verify the fix is supported, put them in a JSON list and run `tools/applyedits.py`. Never trust a checker's fix blindly: one proposed Task tag was wrong.

### Stage 3: per-service coverage checks. STATUS: DONE (3 Nov 2026)
- All coverage groups (cov-d1 to d4, cov-tech, cov-s1 to s8) pass `covcheck`. 34 GAP/THIN additions inserted into 17 files (logged in the Corrections Log); linkcheck 1212 links, 0 bad.
- Deliberately NOT added: Aurora "6 times throughput" line (cov-s4 #2; conflicts with the unresolved 3x/5x figures, settle in Stage 5), cov-tech #36 (duplicate of #21). License Manager soft-limit clause trimmed (quote did not support it).
- Stage 2 leftovers CLOSED 3 Nov 2026: PE5 tags Q34-65 fit their topics, answer keys and domain tables of all five exams are consistent (`pxcheck.py`: no problems, 20/17/15/13 except PE4 19/18/15/13 which is as documented); Lab 7 handler matches the API Gateway payload format 2.0 page (requestContext.http.method, queryStringParameters, statusCode and body). No edits needed.
- NEXT: Stage 4 (second search of the UNSOURCED items; regenerate item files with `review.py items` first so late batches are included).

### Stage 4: second search for unconfirmed claims. STATUS: DONE (3 Nov 2026)
- 13 groups rs1..rs13 (rs11 to rs13 cover the practice exams, cheat sheet, labs and refs). `review.py check rs rsN` prints OK for all. Results are in `S/review/rs_rsN.jsonl` (FOUND with quote, or STILL_UNSOURCED with note). No vault edits were made in this stage.
- Item files were built from the a8467d0 snapshot (`S/v2`). Before Stage 5, refresh `S/v2` to current HEAD or expect `old` text to differ where the vault has since changed (Stage 2/3 edits). Line numbers in ids are from the old snapshot.

### Stage 5: adjudication. STATUS: DONE (4 Nov 2026)
- 13 groups a1..a13 (`S/review/adj_aN.jsonl`, `items_aN.jsonl`), 372 items: 171 APPLY (all applied as `S/fixes/g14.json`, plus 3 follow-ups: Practice Exam 3 line 410, chapter 22 line 305 and the g13 already-applied items), 201 KEEP. `S/v2` refreshed to HEAD 1f6ed43 first. Link check 1212 bad 0, pxcheck no problems. Panorama 20 May 2026 kept (General Reference full_shutdown_services page). WAF Classic is 7 Oct 2026 everywhere. Nothing committed.
- Weakest APPLY: ch17:78 (design opinion deleted, weak evidence). Review in Stage 7.
- For each UNSOURCED claim: APPLY a fix, or KEEP with evidence (distractors, absence from the in-scope list and maths are allowed bases). Rule: never delete a correct exam fact just because a source was hard to find; narrow the wording instead.
- Do: one agent per group, `stage adj (KIND adj)`, then apply every APPLY with `applyedits.py` and log it.
- Known cross-vault items still to settle: "SNS does not store" wording elsewhere (grep), WAF Classic date conflict (7 Oct 2026 vs 30 Sep 2025), Rekognition feature names (Streaming Events vs Streaming Video), DR strategy RPO/RTO figures (diagram only, keep and flag), Quick "evolved from QuickSight", Kendra and Comprehend dates.

### Stage 6: strict re-judging of "supported" entries. STATUS: judging DONE (4 Nov 2026), WEAK adjudication NOT started
- 19 groups j1..j19 (Sonnet agents, `S/review/sup_jN.jsonl` and `rj_jN.jsonl`; brief `S/RJ.md`). 6,854 entries judged, 1,648 WEAK (24%). All WEAK rows with their reasons are in `S/review/weak_all.jsonl`, tagged k = exam (445 practice-exam wrong options and explanations), num (384 claims with numbers, dates, limits) or other (819).
- j14 ran `rjdone` early, so some ids may have both PROVES and WEAK rows: WEAK wins.
- `num` group DONE 4 Nov 2026: 7 groups b1..b7 (`items_bN`, `adj_bN`, brief `S/ADJB.md`), 384 items: 8 edits applied (`S/fixes/g15.json`), 376 KEEP with fuller quotes or maths. Link check 1212 bad 0. `other` sample DONE (100 random, `items_c1/c2`, 5 minor rewordings, `S/fixes/g16.json`); remaining `other` (719) not adjudicated. NOT yet done: `other` remainder and `exam` (445) WEAK groups.
- Most WEAK items mean the quote is incomplete, not that the vault is wrong. Plan: adjudicate `num` first (real risk), then sample `other`, treat `exam` wrong options as distractors unless the stem fact is unsourced. Nothing in the vault changed in this stage yet.
- About 6,100 entries marked SUPPORTED; many rest on loose quotes, especially wrong options in practice exams and self-tests. Build files with `review.py supported GROUP BATCH...`, one agent per group (`stage rj`), then adjudicate every WEAK entry as in Stage 5.

### Stage 7: final independent review. STATUS: DONE (5 Nov 2026)
- Opus reviewer report: `S/review/FINAL_REVIEW.md`. 22 fixes applied (`S/fixes/g17.json`) plus Corrections Log, README, Home and Sources updates. Task B sample: 15 of 100 quotes too thin on their own, none hiding a wrong fact; those 15 ids (ch08:114, pe4a:282, pe2b:51, ch04a:17, ch05:106, ch20:115, pe5b:180, pe4a:285, ch04b:26, ch18:154, ch22:99, ch28:61, pe1a:106, ch26:109, ch10:34) were not re-sourced. Not done on purpose: remaining 719 `other` and 445 `exam` WEAK entries; reviewer items 2.7-2.9 (EFS One Zone cheaper, FSx NTFS, Inspector automated response) left as they are, no source. Nothing committed.
- One `opus` agent (not the one that edited) reviews every changed line (`git diff`), the Corrections Log, and a random sample of 100 SUPPORTED entries against their pages. Recount the checks: 189/189 exam guide items verbatim, 119 in-scope, 50 out-of-scope, 1,210 links, 5 exams x 65 questions, answer keys match, no duplicate stems.
- Then write the final confidence report with the remaining unconfirmed list. Update README, Home, Sources and Corrections Log dates and counts.

## Decisions made (do not redo)

- Lifecycle dates: the General Reference list gives the announcement date; product pages give "closed to new customers" dates. Both are kept and named (Simple AD, Kendra, Snowball Edge, Application Discovery Service).
- VMware Cloud on AWS stays (it is in scope) with the note that AWS no longer resells it.
- Quiz distractors whose reason is unsourced are kept if the keyed answer is sourced and the option is plainly wrong.
- Practice exams keep 20/17/15/13 of 65; the exam overview explains that scored content is 15/13/12/10 of 50.
- Study Guide and Exam Technique `[x]` boxes belong to the user: never change them.
- Memory notes: git in WSL has no GitHub credentials; the user runs pushes and merges.
