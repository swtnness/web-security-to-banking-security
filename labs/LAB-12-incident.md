# Lab 12 — A fictional account-takeover investigation

**Week:** 15. **Type:** tabletop. **Time:** 90–120 minutes. All identifiers and events below are synthetic. Times are UTC within this fictional incident day.

## Evidence packet

| Time | Actor/account | Event | Outcome |
|---|---|---|---|
| 09:00 | U-7 / A-7 | Login attempt | Failed |
| 09:01 | U-7 / A-7 | Login attempt | Failed |
| 09:02 | U-7 / A-7 | Login attempt | Failed |
| 09:03 | U-7 / A-7 | Login with session S-9 | Succeeded |
| 09:04 | U-7 / A-7 | Recovery channel changed | Completed |
| 09:05 | U-7 / A-7 | Beneficiary B-9 added | Completed |
| 09:06 | U-7 / A-7 | Transfer T-1, 90000 fake units | Denied by limit |
| 09:07 | U-7 / A-7 | Transfer T-2, 1000 fake units | Completed |
| 09:08 | U-2 / A-2 | Login attempt | Failed once |
| 09:09 | U-7 / A-7 | Transfer T-2 retry | Same recorded result |
| 09:10 | monitor | Alert on U-7 sequence | Review pending |
| 09:12 | reconciliation | T-2 debit/credit comparison | Matches once |

The packet does not prove a takeover. There is no device fingerprint, customer confirmation or full session linkage for every event.

## Work through the incident

1. Copy the packet into your report or reference it. Build a timeline with facts and a separate hypotheses column.
2. Propose a detection rule combining recovery change, new beneficiary and transfer activity within 10 minutes. Treat this window as an exercise choice.
3. Explain why U-2's single failure does not justify the same action. List one false positive for U-7's pattern.
4. At 09:10, assign fictional owners for triage, session containment, evidence preservation and finance review.
5. State what evidence you would request before restricting more accounts. Use an already verified contact channel in your response design, not the newly changed recovery destination alone.
6. Decide what to verify about T-1 and T-2. T-1 was denied; T-2 completed once. A retry is not a second debit in this packet.
7. Set recovery conditions: verified account access, reviewed recovery changes, correct ledger state and continued observation.
8. Write two engineering improvements and a test for each. Preserve the record of your decisions.

## Expected findings

The combined sequence deserves investigation; the exact cause remains unknown. The retry and reconciliation entries support one recorded T-2 execution, not broad assurance about all transfers. Do not invent a reversal, confirmed attacker or customer loss.

**Save:** timeline, three rules with false positives, a response checklist, facts versus unknowns and two follow-up tests. In the portfolio, label this as a tabletop exercise.

[Week 15](../curriculum/WEEK-15.md)

